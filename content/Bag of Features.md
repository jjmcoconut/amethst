### Methodology
1. Feature Extraction
2. Learn 'visual vocabulary'
3. Quantize features using visual vocabulary
4. Represent images by frequencies of 'visual words'

### Actual Implemented Code (Assignment 5)

Of course it is a simplified version
#### Main function flow

```py
def main():
	vocab = build_vocabulary(train_img_paths, vocab_size, feature)
	train_img_feats = get_bag_of_words(train_img_paths, feature)
	predicted_test_label = svm_classify(train_img_feats, train_labels, test_img_feats, kernel)
	accuaracy = calculate_accuracy(test_true_label, predicted_test_label)
```

1. Build vocabulary
```py
def build_vocabulary(train_img_paths, vocab_size, feature):
	all_feat=[]
	for all img in train_img_paths:
		all_feat.append(feature_extraction(img,feature))
	all_feat = np.concatenate(all_feat,0)
	_,_,centers = cv2.kmeans(all_feat,vocab_size,...)
	return centers
```

- This will sample feature descriptors from the training image, cluster with [[K-Mean Clustering]], return the cluster centers.
- For ```feature_extractions``` we use [[HoG]] or [[SIFT]]
	- To take SIFT value from specific location use
	  ```sift.compute(img,[cv2.KeyPoint(x,y,block_size)])```

2. Get Bag of words
```py
def get_bag_of_words(img_paths,feature):
	vocab = load_vocab_from_feature(feature)
	bag_of_words=[]
	for img in get_img(img_paths):
		img_feat = feature_extraction(img, feature)
		dist = pdist(feature, mvocab)
		hist,_ = np.histogram(np.argmin(dist, axis=1), np.arange(vocab_size+1), density=True)
		bag_of_words.append(hist)
	return np.array(bag_of_words)
```

- This function returns the histogram of features split by vocabulary for each image.

3. Classify using [[SVM]]
```py
def svm_classify(train_img_feats, train_labels, test_img_feats, kernel):
	categories = np.unique(train_labels)
	for cat in categories:
		svm_machine = svm.SVM(kernel,...)
		train_true_label = [0 if cat else 1 for every train_label]
		svm_machine.fit(train_img_feats,np.array(train_true_label))
		prob = svm_machine.predict_..(test_img_feats)
	return predicted_value
```

- We need to modify the regularization parameter of SVM and find the best value. It differs quite a lot.
- Since SVM does not support multi-classification, we will use the one vs others technique and choose the one that returns the largest