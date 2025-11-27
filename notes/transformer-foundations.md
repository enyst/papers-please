#AI-papers
(Yann LeCun)
This leaves out a bunch of prior innovations that *clearly* inspired the transformer authors.

Chief among them is the whole idea of attention, which was popularized by 
"Neural Machine Translation by Jointly Learning to Align and Translate" by
@DBahdanau, @kchonyc, and Yoshua Bengio posted in September 2014.
This is the paper that started the attention craze:
arxiv.org/abs/1409.0473

Self-attention is a clever trick which uses similarities between all pairs of inputs. This makes the network care about relationships between inputs, independently of their order (permutations equivariance). That's the real contribution of the 2017 transformer paper.

But what really boosted the craze was the application of Self-Supervised Learning to transformers, triggered by the 2018 BERT paper, also from Google:
arxiv.org/abs/1810.04805
