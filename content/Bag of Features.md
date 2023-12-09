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

- 