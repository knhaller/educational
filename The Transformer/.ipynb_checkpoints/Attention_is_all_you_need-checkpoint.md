# Attention Is All You Need

#### Notes by: Katie Haller

## Make sure to keep asking the question: WHY???

![The Transformer](./images/AIAYN-Fig.1.png)
*Taken from Attention Is All You Need*

### Embedding

In the embedding, words are represented by vectors. The idea is to create a mapping of the words so that similar words are "close" to each other. For example, we don't want a model to predict "I fed my (car)". We want the model to predict "I fed my (cat)". This way, cats and dogs and say fish are grouped together. So if the model doesn't predict "cat", it will predict "dog". The embedding layer in the encoder "compresses" say a vocabulary of 10k to 300 dimensional dense embeddings. The embedding layer in the decoder would "expand" back to 10k dimensions.

### Positional Encoding

The positional encoders help with relation to other words in the sentence. For example, "The animal didn't cross the street because it was too tired" as humans we know animal and it are the same. The positional encoding would be able to tell you that animal is in the 1st position and it is in the 9th, separated by 8 spaces. The equations used are:

$$PE_{(pos,2i)}=sin(pos/10000^{2i/d_{model}})$$
$$PE_{(pos,2i+1)}=cos(pos/10000^{2i/d_{model}})$$

$pos$ is the position and $i$ is the dimension. The details on how this actually works is tricky. 

### Attention Functions

The paper only mentions two different types of attention, (scaled dot product and multi-head) however, there are actually many more types of attention. Below is a table of popular alignment score functions: 

![Types of Attention](./images/AIAYN-Fig.3.png)
*Taken from the Attention - Attention article*

Since the paper only mentions two attention scores, let's look at those. 

#### Scaled Dot Product

Something that is very important in the Attention paper is actually the attention function. The purpose is to focus on the important words. But the important question is how this is done. One way to help visualize is:

![Attention Score](./images/AIAYN-Fig.2.png)
*Taken from A Simple Explanation of Transformers in NLP*

The dot product attention is much faster and more space efficient than additive attention.

A visualization for this attention function can be seen below:

![Scaled Dot Product](./images/AIAYN-Fig.5.png)

#### Multi-head Attention

![Multi-head Attention](./images/AIAYN-Fig.4.png)
*Taken from Attention Is All You Need*

The main difference between Multi-head attention and scaled dot product is that in the multi-head attention, multiple processes happen simultaneously. The concept of this can be thought of similar to features. The multi-head attention is the main contribution of this paper.

#### Why Self Attention?

![Self Attention](./images/AIAYN-Fig.6.png)
*From Attention Is All You Need*



### Position-Wise Feed-Forward Networks

$$FFN(x)=max(0, xW_{1}+b_{1})W_{2}+b_{2}$$

Resources:

[Attention Is All You Need](https://arxiv.org/pdf/1706.03762.pdf)

[A Simple Explanation of Transformers in NLP](https://towardsdatascience.com/simple-explanation-of-transformers-in-nlp-da1adfc5d64f) - Medium article

[Attention - Attention](https://lilianweng.github.io/lil-log/2018/06/24/attention-attention.html) - Github article