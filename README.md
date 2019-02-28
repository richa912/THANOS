# THANOS

THANOS is a sequence model which captures the two level hierarchy within a document. The first is word level hierarchy and the second is the sentence level hierarchy. The THANOS architecture consists of a tree-LSTM based word level encoder in order to obtain embedding for each sentence in the dataset, a GRU based sentence level encoder and a sentence-level attention layer. However, the limitation of tree-LSTM is that, it does not directly support batched computation. Therefore SPINN (https://arxiv.org/pdf/1603.06021.pdf) is used to implement Tree LSTM at word level to create sentence vectors from the word embedding.

