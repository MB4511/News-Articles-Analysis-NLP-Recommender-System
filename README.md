## News-articles-analysis

As the market for consuming news from digital platforms has shown a sharp rise in past few years, I decided to work on ingesting daily news articles to uncover some interesting insights.


### About Data

The dataset used for this project contains around 200k news headlines from the year 2012 to 2018 obtained from HuffPost. The
features consist of category of news, the headline of news, short description of the article and the date of publication. 

### My approach

I primarily aim to work on two particular aspects of machine learning in theis project:

a) Uncovering Trends from the news articles [with specific interest in Fitness Industry]

b) Building two approaches for recommender system to suggest similar articles to readers

### Part 1 [Trend Analysis in Fitness Industry]

First, I subset the articles corresponding to 'HEALTHY LIVING' and 'WELLNESS' tags/categories to fit under the broader Fitness Category. Then a bunch of different **Natural Language Processing** techniques are applied to gain perspective on how the articles in the fitness industry are being framed. Also it would help us in identifying the keywords which have been used more often in past few years.  

#### Frequent Word Analysis/Bag of Word Approach

To find the most commonly used words in these fitness related articles, I use bag of word approach using the popular **NLTK library** in python.

The stopwords removal becomes a key component to extract meaningful results since extremely common words such as 'an','the',of','is' etc do not provide any insight. 

Moreover, I use a personalized stopword list which is related to fitness world by excluding words like 'fitness','people','world' etc which also are basic vocab, not adding weight to our analysis. 

##### Results: Health, Cancer, Sleep, Stress, Weight are the most common words used in the fitness articles.

#### TF-IDF approach to find more contextual information

Frequent word approach is a good starting point to uncover trends but it focuses too much on mere counts. Contextual analysis is not taken into account. With simple frequency count,
the most frequent words sometimes might tell a story which is expected. TF-IDF approach normalizes the frequency of words by taking the inverse of the document frequency into consideration, 
which penalizes the words which occur more frequently across all the fitness related articles. So words like health, healthy will get lesser importance than sleep or cancer since these words would be appearing
frequently but not as frequently as health, healthy which are likely to appear in every article. 

However, one limitation here is that since there are over 100,000 different words occuring across all the articles, the TF-IDF score for the most contextual word would be low given the sparse nature of the corresponding matrix.
This does not allow the approach to present us with insightful discoveries. 

#### Topic Modeling using LDA approach

Topic modeling technique becomes an effective tool to have in order to uncover hidden semantic structures behind the articles. The intuition behind this approach is to find clusters/topics
based on the distribution of words occuring together across the documents(articles in this case). This really goes a step further to understand the context behind the articles. 

I used TF-IDF vectorizer for the LDA to find this distribution of words as I discussed earlier why count vectorizer approach might lead to unsatisfactory results. 

##### Result: The 10 topics found using the approach gives us interesting insights. Certain topics clearly indicate a particular idea. for example topic 1 includes word distributions from the mental
health world. topic 4 includes keywords pertaining to sleep cycle of humans and topic 6 focuses on cancer study of women working late night shifts. This really gives us information on how articles over the last few years 
have dominated the fitness industry. 

### Part 2 [Designing Recommender System approaches]

A recommender system in this context would help find similarity in articles to engage readers based on their historical reading preferences and when combined with user data, 
similar users could be considered for suggesting a collaborative filtering setup to provide recommendations.

#### Approach 1 [Bag of Word Approach to find similarity in articles]

An euclidean similarity score using pairwise distances between the features of the articles are used to design this recommender approach. So if an article contains words like World Cup, then
other articles on World cup would be recommended to the reader. 

The analysis shows how same word usage in the articles are found effectively by this approach. However, one limitation here is the lack of diversity in the articles. Here
since all the recommended articles have World Cup in it, the articles might be recommended from the same news category, most likely Sports in this case. 

#### Approach 2 [TF-IDF to recommend articles based on context and not just frequent words]

To overcome the above stated challenge, this recommender system approach finds context in various articles to group them together. So now the articles are being judged based on an euclidean similarity score
on basis of TF-IDF score. This allows for recommendations from cross categories of news articles. 

To illustrate this, the results show us that the same article on World Cup now recommends us articles from Entertainment tag with focus on Netflix since an artist who performed in that World Cup
is coming out with a Netflix show. So this is more powerful and diverse recommendation to the reader because even if the reader is a sports fan, he might be interested to read about this exciting
new sports based netflix show. 

### Summary

So through the project, I have discovered few fitness industry trends and got some insights which are challenging to observe given the large volume of data we consume from digital media these days.
For simplicity and less bias, all the articles are from one source. Also, I use some recommender system approaches which could be handy to engage the audience/readers to their preferred choices. Instead of them scrolling to find interesting material,
the recommender system can help them navigate effectively to offer personalized content. However, there could be other important aspects to consider such as the time of article publication, the author writing the articles etc. 

Further works: I would like to incorporate Twitter data along with more recent articles to get more quality data to perform further trend analysis. Also for recommender system, the emerging
deep learning based methods would be used to effectively extract more hidden semantics behind the articles. 






