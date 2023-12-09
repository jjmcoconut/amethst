### Methodology
1. Feature Extraction
2. Learn 'visual vocabulary'
3. Quantize features using visual vocabulary
4. Represent images by frequencies of 'visual words'

### Actual Implemented Code (Assignment 5)

#### Main function flow

```py
def main():
	vocab = build_vocabulary(train_img_paths, vocab_size, feature)
	train_img_feats = get_bag_of_words(train_img_paths, feature)
	predicted_test_img = svm_classify(train_img_feats, train_labels, test_img_feats, kernel)
```

