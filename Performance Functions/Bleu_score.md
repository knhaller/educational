# Bleu Score Notes

#### Katie Haller

Example 1:
French: Le chat est sur le tapis.<br>
Reference 1: The cat is on the mat.<br>
Reference 2: There is a cat on the mat.<br>
MT output: the the the the the the the.

1. Precision:

    Precision would give the output to be $\frac{7}{7}$. 

2. Modified Precision:
    
    The modified precision gives a score of $\frac{2}{7}$ because the first reference only has "the" appear twice.
    
#### Blue score on bigrams
Example 2:<br>
Reference 1: The cat is on the mat.<br>
Reference 2: There is a cat on the mat.<br>
MT output: The cat the cat on the mat.

This is a better output than the one in the first example but still not great.<br>
Possible bigrams:<br>

| Bigrams     | Count       |$Count_{clip}$|
| ----------- | ----------- |----------- |
| the cat     | 2           |  1         |
| cat the     | 1           |   0        |
| cat on      | 1           |  1         |
| on the      | 1           |   1        |
| the mat     | 1           |  1         |


The count is just how many times the bigram appears in the MT output. $Count_{clip}$ is how many times the bigram appears in either of the references. <br><br>
The modified precision is: $\frac{\Sigma(Count_{clip})}{\Sigma(Count)}$. In this case, the modified precision is $\frac{4}{6}$.

$$p_{1}=\frac{\sum_{unigrams \in \hat{y}} Count_{clip} (unigram)}{\sum_{unigram \in \hat{y}} Count(unigram)}$$

Where $\hat{y}$ refers to the output of the MT.

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

Edit: There was an error in Andrew Ng's video. brevity pentalty is supposed to be $1 - \frac{[ref]}{[MT]}$.

Edit 2: In the Bleu score, $p_{n}$ is supposed to be $log(p_{n})$

## Reference:

[Andrew Ng's explanation of Bleu Score](https://www.youtube.com/watch?v=DejHQYAGb7Q)
