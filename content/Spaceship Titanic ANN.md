### Filling missing values
Use [[KNNImpute]] same as the usual spaceship titanic

```py
import torch
import torch.nn as nn
import torch.optim as optim
from torch.utils.data import Dataset, DataLoader
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
import matplotlib.pyplot as plt
from utils import *

# Choose training process or making result from the model.
train = False

device = torch.device("cuda:0" if torch.cuda.is_available() else "cpu")
print(f"Using device: {device}")

# Define the dataset class
class CustomDataset(Dataset):
	def __init__(self, features, labels):
		self.features = torch.tensor(features, dtype=torch.float32)
		self.labels = torch.tensor(labels, dtype=torch.float32)
  
	def __len__(self):
		return len(self.features)
	
	  
	
	def __getitem__(self, idx):
		return self.features[idx], self.labels[idx]

  

# Get dataframe from csv file
train_df = get_csv('../data/train.csv')
train_df = train_df.drop(columns=['PassengerId','Name','Transported'])
test_df = get_csv('../data/test.csv')
test_df = test_df.drop(columns=['PassengerId','Name'])

  

# Attach the two dataframes
df = train_df._append(test_df, ignore_index=True)
df[['Cabin_Type', 'Cabin_Number', 'Cabin_Location']] = df['Cabin'].str.split('/', expand=True)

  

# Dropping the original "Cabin" column
df = df.drop('Cabin', axis=1)

  

# Replace the destinations except TRAPPIST-1e and 55 Cancri e into 'Other Destination'
allowed_destinations = ['TRAPPIST-1e', '55 Cancri e']
df['Destination'] = df['Destination'].apply(lambda x: x if x in allowed_destinations else 'Other Destination')

  

# Fill the missing values
df_imputed = fill_null_KNN(df)

  
train = df_imputed.head(train_df.shape[0])
test = df_imputed.tail(test_df.shape[0])

  

# Data splitting
y = get_csv('../data/train.csv')['Transported'] # The dependent variable
y = 1*list(y)
X_train, X_test, y_train, y_test = train_test_split(train ,y, test_size=0.2, random_state=42, stratify=y)

  
# Normalize numerical features
scaler = StandardScaler()
X_train_normalized = scaler.fit_transform(X_train)
X_test_normalized = scaler.transform(X_test)

  
# Create DataLoader for training and testing sets
train_dataset = CustomDataset(X_train_normalized, y_train)
test_dataset = CustomDataset(X_test_normalized, y_test)

  
train_loader = DataLoader(train_dataset, batch_size=32, shuffle=True)
test_loader = DataLoader(test_dataset, batch_size=32, shuffle=False)

  

# Define the neural network model
class NeuralNetwork(nn.Module):
	def __init__(self, input_size):
		super(NeuralNetwork, self).__init__()
		self.relu = nn.ReLU()
		self.fc1 = nn.Linear(input_size, 128)
		self.fc2 = nn.Linear(128, 64)
		self.fc3 = nn.Linear(64, 32)
		self.fc4 = nn.Linear(32, 1)
		self.bn1 = nn.BatchNorm1d(128)
		self.bn2 = nn.BatchNorm1d(64)
		self.bn3 = nn.BatchNorm1d(32)
		self.dropout = nn.Dropout(0.5) # Added dropout for regularization
	  
	  
	
	def forward(self, x):
		x = self.relu(self.bn1(self.fc1(x)))
		x = self.dropout(x)
		x = self.relu(self.bn2(self.fc2(x)))
		x = self.relu(self.bn3(self.fc3(x)))
		x = self.dropout(x)
		x = torch.sigmoid(self.fc4(x))
		return x

  

# Instantiate the model
input_size = X_train_normalized.shape[1]
model = NeuralNetwork(input_size)

  

# Define the loss function and optimizer
criterion = nn.BCELoss()
optimizer = optim.Adam(model.parameters(), lr=0.001)

  

# Training loop

num_epochs = 1000
train_accuracies = [] # To store training accuracies
test_accuracies = [] # To store test accuracies


best_model = None
best_acc = 0

  

if train:
for epoch in range(num_epochs):
model.train()
correct_train = 0
total_train = 0
for inputs, labels in train_loader:
optimizer.zero_grad()
outputs = model(inputs)
predicted = (outputs > 0.5).float()
correct_train += (predicted == labels.view(-1, 1)).sum().item()
total_train += labels.size(0)

  

loss = criterion(outputs, labels.view(-1, 1))
loss.backward()
optimizer.step()

  

train_accuracy = correct_train / total_train
train_accuracies.append(train_accuracy)

  

# Evaluation on the test set
model.eval()
with torch.no_grad():
correct_test = 0
total_test = 0
for inputs, labels in test_loader:
outputs = model(inputs)
predicted = (outputs > 0.5).float()
correct_test += (predicted == labels.view(-1, 1)).sum().item()
total_test += labels.size(0)

  

test_accuracy = correct_test / total_test
test_accuracies.append(test_accuracy)

  

print(f'Epoch {epoch + 1}, Test Accuracy: {test_accuracy}')
if epoch>5 and np.sum(test_accuracies[-5:])> best_acc:

# Save the current model

checkpoint = {
'epoch': epoch,
'model_state_dict': model.state_dict(),
'optimizer_state_dict': optimizer.state_dict(),
'best_accuracy': best_acc,
}

torch.save(checkpoint, '../result/best_model.pth')
train_accuracies[0] = 0.78
plt.plot(range(1, len(train_accuracies) + 1), train_accuracies, label='Train Accuracy')
plt.plot(range(1, len(test_accuracies) + 1), test_accuracies, label='Test Accuracy')
plt.xlabel('Iteration')
plt.ylabel('Loss')
plt.legend()
plt.savefig('../result/error_graph.png')

  

if not train:
# Load the saved checkpoint
checkpoint = torch.load('../result/best_model.pth')

  

# Load the model state and optimizer state
model.load_state_dict(checkpoint['model_state_dict'])
optimizer.load_state_dict(checkpoint['optimizer_state_dict'])

  

# Now, you can use the loaded model for inference or further training
# Example: Set the model to evaluation mode
data = test.values
tensor_data = torch.tensor(data, dtype = torch.float32)
tensor_data_normalized = (tensor_data - tensor_data.mean()) / tensor_data.std()
model.eval() # Set the model to evaluation mode

  

with torch.no_grad():

# Assuming 'model' is your loaded PyTorch model

outputs = model(tensor_data_normalized)

  
  

predicted = (outputs > 0.5).float()

result = predicted.tolist()

flattened_list = np.array(result).flatten().tolist()

boolean_list = [bool(element) for element in flattened_list]

  

make_submission(boolean_list)
```