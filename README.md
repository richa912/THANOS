# THANOS

THANOS is a sequence model which captures the two level hierarchy within a document. The first is word level hierarchy and the second is the sentence level hierarchy. The THANOS architecture consists of a tree-LSTM based word level encoder in order to obtain embedding for each sentence in the dataset, a GRU based sentence level encoder and a sentence-level attention layer. However, the limitation of tree-LSTM is that, it does not directly support batched computation. Therefore SPINN (https://arxiv.org/pdf/1603.06021.pdf) is used to implement Tree LSTM at word level to create sentence vectors from the word embedding.


Data explanation is as following:
1. Yelp review dataset (raw_150k.csv) consisting of 150k reviews is in path Data/Yelp Raw Data.
2. Text review column (Data/Input Data) from raw_150k.csv is used to create parse trees (Data/Binary Tree Output) using the jar file in the path Data/Binary Tree Jar File. The jar file is created using Stanford tree parser with some NLP preprocessing tasks.
3. Binary tree output is used to create 3 pickle files (Data/Pickle File) named yelp_unk150k.pkl, yelp_parsedtree150k and vocab.pkl.
   - yelp_parsedtree150k.pkl consits of parsed trees for the reviews.
   - yelp_unk150k.pkl consists of list of tokens for each repective tree. The token list consist of the words in the tree in sequential order. the words with less than 5 frequency in the vocab list of the dataset is replace by 'unk' token. 
     - For example : ( ( ( ( i ( ( excepted ( a lot ) ) ( from ( this movie ) ) ) ) , ) and ) ( it ( did deliver ) ) ) . )
     - token list for above tree will be: ['i', 'expected', 'a', 'lot', 'from', 'this', 'movie', ',', 'and', 'it', 'did', 'deliver']
   - vocab.pkl file consists of all the unique words in the tokens created from trees which will be used to create the dictionary of words in our dataset.


After preparing the tree, token , and vocab file we are ready to feed this data to train our model. Below are the steps:
1. python notebook creating_train_test_dev_files.ipynb is used to create train, dev and test pickle files from yelp_parsedtree150k.pkl and yelp_unk150k.pkl files. 
   - Open the jupyter notebook and run all the cells of python notebook creating_train_test_dev_files.ipynb.

2. python notebook run_model.ipynb consists of commands to create the vocab json file using python file build_vocab.py and train the model using python file train.py. The commands are as below:
```
- %run build_vocab.py --data_dir Data/Pickle File (from jupyter notebook)
- %run train.py --data_dir Data --model_dir experiments/base_model (from jupyter notebook)
```
