Neural Sentiment Classification
==========

Neural Sentiment Classification aims to classify the sentiment in a document with neural models, which has been the state-of-the-art methods for sentiment classification. In this project, we provide our implementations of NSC [Chen et al., 2016], NSC+LA [Chen et al., 2016] and NSC+UPA [Chen et al., 2016] in which user and product information is considered via attentions over different semantic levels.

Evaluation Results
==========

Evaluation results on document-level sentiment classification. Acc.(Accuracy) and RMSE are the evaluation metrics.
![image](https://github.com/huimchen/figure/blob/master/evaluation%20results.png)

In the above table, baseline models including Majority, Trigram, TextFeature, UPF, AvgWordvec, SSWE, RNTN + RNN, Paragraph Vector, JMARS and UPNN are reported in [Tang et al., 2015].

Data
==========

We provide IMDB, Yelp13 and Yelp14 dataset we used for sentiment classification in data/ directory. We propocess the original data to make it satisfy the input format of our codes. The original datasets are released by the paper "Learning Semantic Representations of Users and Products for Document Level Sentiment Classification." [[Download]](http://ir.hit.edu.cn/~dytang/paper/acl2015/dataset.7z)

Pre-trained word vectors are learned on each dataset (IMDB, Yelp13, Yelp14) separately.

To run our NSC and NSC+LA model, the dataset should be put in the folder data/XX/ using the following format, containing five files:
+ train.txt: training file, format (userid	productid	class	document), split by '\t'.
+ dev.txt: dev file, same format as train.txt.
+ test.txt: test file, same format as train.txt.
+ wordlist.txt: corresponding words with same sequence in pre-trained word vectors, one per line.
+ embinit.save: the pre-trained word embedding file, which is saved as pickle and can be loaded from pickle to numpy arrays.

To run our NSC+UPA model, the dataset should be put more two files in the folder data/XX/ using the following format:
+ usrlist.txt: user ids in each dataset, per one line.
+ prdlist.txt: product ids in each dataset, per one line.

where 'XX' is the corresponding dataset name. For example, 'XX' could be IMDB', 'yelp13', 'yelp14' in this project.

Codes
==========

The source codes of various models are put in the folders NSC/src, NSC+LA/src, NSC+UPA/src.


Train
==========

For training, you need to type the following command in the folder src/ of each model:

	THEANO_FLAGS="floatX=float32,device=gpu" python train.py $dataset $class

where *dataset* is the corresponding dataset folder, *class* is the number of corresponding domain.

For example, we use the following command when classfing the IMDB document:

	THEANO_FLAGS="floatX=float32,device=gpu" python train.py IMDB 10

The training model file will be saved in the folder model/bestmodel/ of each model.

Test
==========

For testing, you need to type the following command in the folder src/ of each model:

	THEANO_FLAGS="floatX=float32,device=gpu" python test.py $dataset $class

where *dataset* is the corresponding dataset folder, *class* is the number of corresponding domain.

For example, we use the following command when classfing the IMDB document:

	THEANO_FLAGS="floatX=float32,device=gpu" python test.py IMDB 10

The testing result which reports the Accuracy and RMSE will be shown in screen.

Cite
==========

If you use the code, please cite the following paper:
[Chen et al., 2016] Huimin Chen, Maosong Sun, Cunchao Tu, Yankai Lin and Zhiyuan Liu. Neural Sentiment Classification with User and Product Attention. In proceedings of EMNLP.[[pdf]](http://www.thunlp.org/~chm/publications/emnlp2016_NSCUPA.pdf)

Reference
==========
[Tang et al., 2015] Duyu Tang, Bing Qin, Ting Liu. Learning Semantic Representations of Users and Products for Document Level Sentiment Classification. In Proceedings of EMNLP.
