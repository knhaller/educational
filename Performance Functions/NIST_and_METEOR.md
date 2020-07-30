# NIST and METEOR

#### Notes by: Katie Haller

BLEU has a few downsides to it - it doesn't consider importance of words. For example, here are some reference sentences:

> Orejuela appeared calm as he was lead to the American plane which will take him to Miami, Florida.

> Orejuela appeared calm while being escorted to the plane that would take him to Miami, Florida.

> Orejuela appeared calm as he was being led to the American plane that was to carry him to Miami in Florida.

> Orejuela seemed quite calm as he was being led to the American plane that would take him to Miami in Florida.

#### Some machine generated translations:

> Appeared calm when he was taken to the American plane, which will to Miami, Florida.

> which will he was, when taken appeared calm to the American plane to Miami, Florida.

The problem with the first generated sentence is that the person's name is dropped out and there is to verb after "will". The problem in the second sentence is pretty much everything, it's nonsense. However, they both have the same BLEU scores.<sup>[2](#myfootnote2)</sup> 

## What is NIST?

"NIST is a variant of BLEU that weights n-gram matches by their information gain, i.e., it indi- rectly penalizes uninformative n-grams." - DialoGPT<sup>[1](#myfootnote1)</sup>

## What is METEOR?

Resources:

<a name="myfootnote1">1</a>: [DialoGPT](https://arxiv.org/pdf/1911.00536.pdf)

<a name="myfootnote2">2</a>: [Evaluating Text Output in NLP: BLEU at your own risk](https://towardsdatascience.com/evaluating-text-output-in-nlp-bleu-at-your-own-risk-e8609665a213)

https://arxiv.org/pdf/1601.02789.pdf