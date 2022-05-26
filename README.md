# Analysis Of Lyrics For Different Music Genres


## ABSTRACT
Song lyrics can be the center focus of a song, or a secondary feature of a great
instrumental song. With the centralization of songs and their lyrics on the internet, this
gives people a great opportunity to conduct a meta analysis on patterns that artists take
to be a part of a certain genre. For this project, I analyzed 6 genres (Hip Hop, Sertanejo,
Rock, Pop, and Samba) to answer the overall question; What are the similarities and
differences of lyrics between different musical genres? The results showed that
there are definitive differences between Hip Hop and all other genres in regards to
sentiment and lyric topics. It is clear that various dance genres like Samba Sertanejo,
and Funk Carioca do not focus on complicated words, and generally keep the mood
light and simple.
## Analysis of Genre’s Lyrics
#### Data Description and Transformation
The following dataset used was downloaded from [Kaggle](https://www.kaggle.com/datasets/neisse/scrapped-lyrics-from-6-genres), which contains both a
dataset full of lyrics for each artist, and artist metadata, such as general genre and
language spoken. The dataset was web scraped from the website [Vagalume](https://www.vagalume.com.br/), which is a
brazilian music website, which contains many different languages and genres.
In order to analyze this data, it was necessary to transform all languages into English,
so the first major transformation was translating all Non-English languages using a
[Google Translate API](https://cloud.google.com/translate). The dataset consisted mostly of English, but other languages
were present

**Figure 1. Distribution Of Languages Before Sampling**


![](https://github.com/GrantRedfield/MusicGenreLyricAnalysis/blob/main/images/Figure_1.png)


The second transformation was a reduction in songs to analyze. I sampled 500 songs in
each genre to give an equal representation. This reduction helped speed up runtime,
especially when conducting Principal Component Analysis (PCA).
## Principal Component Analysis
The first analysis conducted on our dataset was PCA. We took our TFIDF table, bagged
our dataset by artist and compared the first most significant principal components
against each other. Below you can see each artist highlighted by their dominating
Genre.


**Figure 2. PC0 vs PC1 For All Genres**
![](https://github.com/GrantRedfield/MusicGenreLyricAnalysis/blob/main/images/PCA.jpg)



The first noticeable observation is that Hip Hop, Rock, and Pop contribute to the most
variance in PC0. Samba, Sertanejo and Funk Carioca are extremely clustered
compared to the other three, which seem to be equally spread out on the PC0 axis. This
indicates that the differences in language vary much more for the first three than the
latter. It should also be noted that Samba, Sertanejo and Funk Carioca are the majority
of our Spanish and Portuguese songs.
## Genre Topics
Conducting Latent Dirichlet Allocation (LDA), I was able to discover common topics
grouped by genre. Assuming 30 total topics, the LDA model distributed the probability
that each topic was being discussed per genre. Below are the most significant findings


**Figure 3. Hip Hop’s Top Topics**
![](https://github.com/GrantRedfield/MusicGenreLyricAnalysis/blob/main/images/Figure_3_Hip_Hop.jpg)
                   



**All Other Genres Cross Over Topic**


**Figure 4. Topic #3 Intersection Topic**
![](https://github.com/GrantRedfield/MusicGenreLyricAnalysis/blob/main/images/Figure_4.jpg)

Hip hop stood out from the other genres as the most unique. The words in the topics
seemed to be aggressive and more diverse than other genres such as Sertanejo.
Topic #3 seemed to be the intersection of all of these genres except Hip Hop. Love, Life,
and Heart appear in many topics, which can be interpreted as light hearted and
somewhat simple.
Using clustering, we can see certain topics have various themes, and can generally
align with a certain genre.

**Figure 5. Clustering of All Genre Topics**
![](https://github.com/GrantRedfield/MusicGenreLyricAnalysis/blob/main/images/Figure_5.png)

The purple line indicates Hip Hop, while the other colors are a mixture of our other 5
genres. We can see that the Red, green, and orange lines are more closely related to
each other.
Word Embeddings
The next piece of analysis was to group together similar words within each Genre to
build on the Topics discovered.


**Figure 6. Hip Hops Word2Vec Scatter Plot**
![](https://github.com/GrantRedfield/MusicGenreLyricAnalysis/blob/main/images/Figure_6.png)


**Figure 7. Samba’s Word2Vec Scatter Plot**
![](https://github.com/GrantRedfield/MusicGenreLyricAnalysis/blob/main/images/Figure_7.png)


**Figure 8. Rock’s Word2Vec Scatter Plot**
![](https://github.com/GrantRedfield/MusicGenreLyricAnalysis/blob/main/images/Figure_8.png)

We can see that Hip Hop’s distribution (Figure 6) contains more dense, and more closely related
words than Samba’s (Figure 7). It is interesting to see a few different clusters in Figure 6.
Money, time and a couple explicit words seem to be related, as well as love, girl and baby.
Figure 7 appears to be equally distant words, ones that are non-descriptive and quite simple.
This further indicates to me that Samba does not have a preference of similar words. Figure 8
has a couple of interesting clusters; Love and want are extremely close to each other, while
never and feel overlap. This seems like a dichotomy that the genre Rock can possess.
Considering that Rock was widely distributed across our PCA graph (Figure 2), this indicates to
me that Rock can possess different philosophies/meanings in regards to emotions per artist.

## Sentiment Analysis
The last analysis is determining the general sentiment of each genre. I used a lexicon
file, salex_nrc.csv, to identify 8 different emotions within the lyrics; Anger, Anticipation,
Disgust, Fear, Joy ,Sadness, Surprise and Trust. After mapping each term in our lyrics
to the lexicon file, we are able to aggregate our lyrics to a Genre level and look from a
high level point of view.


**Figure 9. Heatmap of Sentiments Across Genres**
![](https://github.com/GrantRedfield/MusicGenreLyricAnalysis/blob/main/images/Figure_9.png)

The numbers above (Figure 9) represent the average occurrence of each emotion for all
genres. The heatmap gives a clear indication, especially that Samba, Sertanjeo and
Pop have a much wider occurrence of Joy than Rock or Hip Hop. There is also a distinct
difference of the emotions Anger and Disgust when comparing the different genres.
Samba, Sertanejo, and Pop do not appear to touch these emotions, while the other
three genres have

**Figure 10. Polarity of Each Genre**
![](https://github.com/GrantRedfield/MusicGenreLyricAnalysis/blob/main/images/Figure_10.png)

The figure above (Figure 10) shows us the polarity aggregated by each genre. The
polarity is the total summation of emotions, a negative emotion term flagged as -1 and a
positive emotion flagged as +1. After taking the average polarity across the genre, we
can now see what the general sentiment is, and the results are fascinating.
Hip Hop is the most negative, and amba, Sertanejo, and Pop are clearly positive. Rock
can clearly swing either way, and based off of the previous research this coincides with
the Word2Vec results as well as the LDA topics.

## Conclusions
After the conducted research, we can conclude a couple of general patterns around the
genres available in our dataset.

● Hip Hop appears to have the most diverse and expressive language between our
6 genres, and at the same time has the most negative emotion put into the lyrics.

● Samba, Funk Carioca , and Sertanejo generally have simple lyrics and tend to be
more positive. This is likely due to more focus on the instrumental aspect of the
songs, encouraging dance rather than passive listening.

● Rock covers the widest range of emotions, and gives a diverse range of words to
describe the topics at hand

● Pop general generally has positive and lighthearted lyrics.
Limitations And Future Research

The dataset clearly limited us to 6 genres, so certain findings could be biased based off of our
current available genres. The translation of Portuguese and Spanish songs may have limited
the artists true words and emotions put into the songs. For future research, we hope to expand
this analysis to more genres to include a more diverse set of lyrics and ideas.

