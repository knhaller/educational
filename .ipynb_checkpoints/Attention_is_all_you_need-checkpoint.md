# Attention Is All You Need

### Notes by: Katie Haller

![The Transformer](./images/AIAYN-Fig.1.png)

#### Embedding

In the embedding, words are represented by vectors. The idea is to create a mapping of the words so that similar words are "close" to each other. For example, we don't want a model to predict "I fed my (car)". We want the model to predict "I fed my (cat)". This way, cats and dogs and say fish are grouped together. So if the model doesn't predict "cat", it will predict "dog". The concept makes sense, however, the details of how this happens are still fuzzy. It will make more sense when I look at the details in the code.

#### Positional Encoding

The positional encoders help with relation to other words in the sentence. The equations used are:

$$PE_{(pos,2i)}=sin(pos/10000^{2i/d_{model}})$$
$$PE_{(pos,2i+1)}=cos(pos/10000^{2i/d_{model}})$$

$pos$ is the position and $i$ is the dimension. So what does this actually mean? We know both $sin$ and $cos$ oscillate between -1 and 1.

#### Attention Functions

Something that is very important in the Attention paper is actually the attention function. The purpose is to focus on the important words. But the important question is how this is done. One way to help visualize is:

![Attention Score](./images/AIAYN-Fig.2.png)

The paper only mentions two different types of attention, (scaled dot product and multi-head) however, there are actually many more types of attention. Below is a table of popular alignment score functions: 

![Types of Attention](./images/AIAYN-Fig.3.png)

Since the paper only mentions two attention scores, let's look at those. 

Resources:

[Attention Is All You Need](https://arxiv.org/pdf/1706.03762.pdf)

[A Simple Explanation of Transformers in NLP](https://towardsdatascience.com/simple-explanation-of-transformers-in-nlp-da1adfc5d64f) - Medium article

[Attention - Attention](https://lilianweng.github.io/lil-log/2018/06/24/attention-attention.html) - Github article