# THANOS

THANOS is a sequence model which captures the two level hierarchy within a document. The first is word level hierarchy and the second is the sentence level hierarchy. The THANOS architecture consists of a tree-LSTM based word level encoder in order to obtain embedding for each sentence in the dataset, a GRU based sentence level encoder and a sentence-level attention layer. However, the limitation of tree-LSTM is that, it does not directly support batched computation. Therefore SPINN (https://arxiv.org/pdf/1603.06021.pdf) is used to implement Tree LSTM at word level to create sentence vectors from the word embedding.


Data explaiation is as following:
1. Yelp review dataset (raw_150k.csv) consisting of 150k reviews is in path Data/Yelp Raw Data.
2. Text review text column (Data/Input Data) from raw_150k.csv is used to create parse trees (Data/Binary Tree Output) using the jar file in the path Data/Binary Tree Jar File. The jar file is created using Stanford tree parser with some NLP preprocessing tasks.
3. Binary tree output is used to create 3 pickle files (Data/Pickle File) named yelp_unk150k.pkl, yelp_parsedtree150k and vocab.pkl. yelp_unk150k.pkl consists of list of tokens for each repective review row.
For example : 'The food was good. But I didn't like the ambience.'
token list for above review will be: ['The', 'food', 'was', 'good', '.', 'But', 'I', "didn't", 'like', 'the', 'ambience', '.']
yelp_parsedtree150k consits of parsed trees for the reviews. vocab.pkl file consists of all the unique words in the dataset whic will be used to create the dictionary of words in our dataset.


