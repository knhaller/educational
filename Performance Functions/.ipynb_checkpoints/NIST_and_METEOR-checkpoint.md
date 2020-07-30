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

The problem with the first generated sentence is that the person's name is dropped out and there is to verb after "will". The problem in the second sentence is pretty much everything, it's nonsense. However, they both have the same BLEU scores.<sup>[2](#whyBleuIsBad)</sup> 

## What is NIST?

"NIST is a variant of BLEU that weights n-gram matches by their information gain, i.e., it indi- rectly penalizes uninformative n-grams." - DialoGPT.<sup>[1](#DialoGPT)</sup> Essentially, they have heavier weights with more rare words. You can see this below: 

![NIST Formula](./images/NIST-Fig.1.png)
<sup>[3](#bleuAndNistPPT)</sup>

It is noted that $w_{n} = \frac{1}{N}$. The number of occurrences of $w_{1}...w_{n-1}$ are at least as many as $w_{1}...w_{n}$. So the value of $Info(w_{1}...w_{n})$ will be at minumum 0. 

The NIST paper describes the BLEU score as:

![Bleu score formula](./images/NIST-Fig.2.png)
<sup>[4](#originalNist)</sup>

Comparing this with the Bleu score formula written out differently, we can see:

The n-gram (instead of unigram) would be as follows:

$$p_{n}=\frac{\sum_{ngrams \in \hat{y}} Count_{clip} (ngram)}{\sum_{ngram \in \hat{y}} Count(ngram)}$$

\begin{equation}
  BP=\begin{cases}
    1, & \text{if $[MT]>[ref]$}.\\
    exp(1-\frac{[ref]}{[MT]}), & \text{otherwise}.
  \end{cases}
\end{equation}

where $[ref]$ is the reference output length and $[MT]$ is the MT output length.

$$Bleu=(BP)(exp[\frac{1}{N}\sum_{n=1}^{N}log(p_{n})])$$

One question I have is are these two the same? Well let's see. So $BP$ can be rewritten as: $BP = exp(max(0, (1 - \frac{[ref]}{[MT]})))$. As $exp(0) = 1$. So, $Bleu$ can be rewritten as:

$$Bleu = exp(max(0, (1 - \frac{[ref]}{[MT]})))(exp[\frac{1}{N}\sum_{n=1}^{N}log(p_{n})])$$

$$Bleu = (exp[\frac{1}{N}\sum_{n=1}^{N}log(p_{n})])(-1*exp(max(0, \frac{[ref]}{[MT]} - 1)))$$

$$Bleu = exp([\frac{1}{N}\sum_{n=1}^{N}log(p_{n})]-max(0, \frac{[ref]}{[MT]} - 1))$$

$w_{n} = \frac{1}{N}$

$$Bleu = exp([\sum_{n=1}^{N}w_{n}log(p_{n})]-max(0, \frac{[ref]}{[MT]} - 1))$$

## What is METEOR?

> "METEOR is similar to BLEU but includes additional steps, like considering synonyms and comparing the stems of words (so that “running” and “runs” would be counted as matches). Also unlike BLEU, it is explicitly designed to use to compare sentences rather than corpora"<sup>[2](#whyBleuIsBad)</sup>

![Fmean](./images/METEOR-Fig.1.png)
<sup>[6](#METEOR)</sup>

P is unigram precision and R is unigram recall.

![Penalty](./images/METEOR-Fig.2.png)
<sup>[6](#METEOR)</sup>

> "First, all the unigrams in the
system translation that are mapped to unigrams in
the reference translation are grouped into the fewest possible number of chunks such that the unigrams in each chunk are in adjacent positions in
the system translation, and are also mapped to unigrams that are in adjacent positions in the reference
translation."<sup>[6](#METEOR)</sup>

> "For example, if the system translation was “the
president spoke to the audience” and the reference
translation was “the president then spoke to the
audience”, there are two chunks: “the president”
and “spoke to the audience”. Observe that the penalty increases as the number of chunks increases to
a maximum of 0.5. As the number of chunks goes
to 1, penalty decreases, and its lower bound is decided by the number of unigrams matched."<sup>[6](#METEOR)</sup>

![Score](./images/METEOR-Fig.3.png)
<sup>[6](#METEOR)</sup>


Resources:

<a name="DialoGPT">1</a>: [DialoGPT](https://arxiv.org/pdf/1911.00536.pdf)

<a name="whyBleuIsBad">2</a>: [Evaluating Text Output in NLP: BLEU at your own risk](https://towardsdatascience.com/evaluating-text-output-in-nlp-bleu-at-your-own-risk-e8609665a213)

<a name="bleuAndNistPPT">3</a>: [Machine Translation Evaluation](https://www2.spsc.tugraz.at/www-archive/AdvancedSignalProcessing/WS06-MachineTranslation/MTEvaluation_Sakir.pdf)

<a name="originalNist">4</a>: [Automatic evaluation...](http://www.mt-archive.info/HLT-2002-Doddington.pdf)

<a name="comparingScores">5</a>: [Comparison and Adaption...](https://arxiv.org/pdf/1601.02789.pdf)

<a name="METEOR">6</a>: [METEOR](https://www.cs.cmu.edu/~alavie/papers/BanerjeeLavie2005-final.pdf)
