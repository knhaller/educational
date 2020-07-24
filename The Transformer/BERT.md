# BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding

#### Notes by: Katie Haller

![BERT architecture](./images/BERT-Fig.1.png)
<sup>[1](#myfootnote1)</sup>

During the pre-training, the model is trained on unlabeled data. Later, the parameters are fine-tuned with labeled data from the downstream tasks.

Things to note about the figure above:
- C is a binary output for the next sentence prediction (NSP). It outputs a 1 if sentence B follows sentence A in context, and 0 otherwise.<sup>[2](#myfootnote2)</sup>
An example of this is: 
![Is sentence next](./images/BERT-Fig.3.png)
<sup>[1](#myfootnote1)</sup>
- Some words are masked 
A portion of those words are unchaged:
![Masked words](./images/BERT-Fig.4.png)
<sup>[1](#myfootnote1)</sup>

![BERT input representation](./images/BERT-Fig.2.png)
<sup>[1](#myfootnote1)</sup>

The segment embedding identifies if it's sentence A or B. The token embeddings can be viewed as word embeddings, except instead it is applied after WordPiece. The position embedding is added for the position in the sequence.

![BERT architecture](./images/BERT-Fig.5.png)
<sup>[4](#myfootnote4)</sup>

The BERT base is made up of 12 Transformer encoders.

In fine-tuning, the learning rate and batch size are less than pre-training.

Resources:

<a name="myfootnote1">1</a>: [BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding](https://arxiv.org/pdf/1810.04805.pdf)

<a name ="myfootnote2">2</a>: [BERT Explained](https://www.youtube.com/watch?v=xI0HHN5XKDo)

<a name="myfootnote3">3</a>: [BERT Explained – A list of Frequently Asked Questions](https://yashuseth.blog/2019/06/12/bert-explained-faqs-understand-bert-working/#:~:text=The%20input%20representation%20used%20by,classification%20token%20%E2%80%93%20%5BCLS%5D.)

<a name="myfootnote4">4</a>: [The Illustrated BERT](http://jalammar.github.io/illustrated-bert/)