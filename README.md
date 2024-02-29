### Tanner Zuleeg (1/4/24)
___
### Topic Backgrounds
Nihilism is the rejection of all religious and moral principles, believing that life is meaningless. Existentialism, as a response to nihilism, posits that meaning not only can exist but is entirely of our own making. Facets of both existentialism and nihilism have always existed, but it was not until the scientific revolution reached its full stride in the early 19th century, challenging religious and notions of a meaningful life, that they began widespread cultural development. Nihilism and existentialism are very similar in rejecting objective meaning, often leading to depressive thinking, pessimism, and apathy. However, they differ in their implications of no objective meaning: nihilism suggests life is something to be endured, while existentialism emphasizes the imperative to fight for the creation of subjective meaning in life.

### Problem Statement
In this project, I aim to explore the similarities and differences between nihilism and existentialism through the language used by their adherents. To accomplish this, I will use various NLP models to analyze the kinds of words used in each subreddit and, in the end, build a predictive model. Success will be evaluated based on accuracy and precision. The conclusions of this project are expected to impact anyone interested in meaningful living.

### Exploratory Data Analysis
I collected text from 7924 posts across the subreddits nihilism and existentialism in roughly equal proportion. Many posts only had a title and no body text (almost 3000 of them), so I combined the title and body, creating a separate column for this aggregated text data. The first thing that stood out to me was the word count distribution of the two subreddits. Existentialism has an average word count of 128.50, and nihilism has an average word count of 75.92. This is good because we can use word count as a predictor in a model. The second thing I noticed is that the most frequent words from both subreddits have considerable overlap: life, meaning, just, people, think, feel, world, know. However, there are some differences in this list; existentialism uses 'death' much more than nihilism, and conversely, nihilism uses 'want' and 'really'.

![Top 15 Existentialist Words](./images/top_15_existentialist.png)
![Top 15 Nihilist Words](./images/top_15_nihilist.png)

Next, I looked at the most frequent bigrams in both subreddits. Again, there is quite a bit of overlap. Both subreddits use 'don know', 'meaning life', and 'feel like'. However, the existential subreddit uses 'live life' and 'makes sense,' while the nihilist subreddit uses 'doesn't matter' and 'objective meaning'.

![Top 15 Existentialist Words](./images/top_15_existentialist2.png)
![Top 15 Nihilist Words](./images/top_15_nihilist2.png)

### Models
We fitted three different models. First, count vectorizer with a logistic regression classifier, which got an accuracy score of 77.18%. TFIDF with logistic regression got an accuracy score of 77.84%, and finally, a TFIDF vectorizer with a multinomial naive Bayes classifier got the lowest accuracy score of 73.14%. For the first two models, I looked at the top 10 most significant words in the model. As we might expect, some of the top significant words of the model are 'nihilist' and 'existentialist,' but also words such as 'Camus' and 'Sartre,' both proper nouns of monumental figures in the field (Sartre, for example, coining the term 'existentialist' itself) dealing with 'depression.'

The TFIDF vectorizer and the Count vectorizer have accuracies that are too close to call. To make the final decision about which model to continue with, I looked at classification reports for each and saw that TFIDF had higher precision. This will be the one we will add predictors too.

![TFIDF Model Performance](./images/CMTFIDF.png)

### Feature Selection
We will add two predictors: 'sentiment' and 'word count.' Sentiment analysis could be interesting here because of the nature of the subject material of the subreddits. Word count might also be a good predictor because we saw earlier that there is a large discrepancy between the average word counts between the subreddits.

After we add these features, our accuracy actually goes down quite a bit to 66%.

### Conclusions
While it is unfortunate that the addition of these predictors contributed to model performance, I am very happy with the model accuracy of the original TFIDF model. From the fact a model was able to achieve nearly 78% accuracy on two VERY similar subreddits, along with certain most common word and bigrams being part of the predictors, we can conclude that the main way to distinguish the two models are the use of the words 'nihilism,' 'existentialism,' 'meaning,' 'meaning life,' 'don't know,' etc. This is what makes nihilism and existentialism distinguishable. We can also see that linguistic analysis of the diction in each subreddits are much stronger predictors that notions of sentiment score or even word count. I find this result very satisfactory and interesting because this model was trained on data from user posts, not intellectuals, not books, not articles. These are the noisy posts of people who have an internet connection and the inclination to spend time on these subreddits while using it. And yet, through this noise, we find predictability.
