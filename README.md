# Sentiment Evolution of Movie Transcripts
---
![Joker_evolution](https://raw.githubusercontent.com/kcandost/TDI_Capstone/master/img/Joker_evolution.jpg)

### Motivation

Entertainment industry each year loses hundreds of millions of dollars over poor investments into projects. In 2021 alone, box office lost over   [700 million dollars]( https://en.wikipedia.org/wiki/List_of_biggest_box-office_bombs) over several movies. Streaming industry suffers from the same problem. Last year more than 100 shows are cancelled  and most of which due to poor rating scores. Therefore an ability to predict the success of a title to a reasonable degree can save a lot of time and money to everyone involved.

I wanted to test the strength of 'Sentiment Evolution' of a movie script as a metric for its success, and to provide a tool for both writers and producers to be able to predict how successful a transcript can be based on its sentiment evolution.

### Data Ingestion
I scraped [imdb.com](https://www.imdb.com/) for genre and score and [imsdb.com]( https://imsdb.com/) for the movie transcripts for 900 movies using BeautifulSoup and web requests.
  * I performed data cleaning and preprocessing using standard NLP tools.
  * I chose NRCLex for the supervised NLP model to perform sentiment analysis.
  * Main tools: Pandas, Beatifulsoup, Requests, Matplotlib, NLP libraries (nltk, NRCLex).
### Model 
There are 10 basis dimensions in NRC Lexicon: Positive, Negative, Anger, Trust, Anticipation, Joy, Fear, Sadness, Surprise, and Disgust. The feature matrix is constructed by applying the following workflow for each movie:
 * Preprocessing the transcript
 * Splitting into 12 pieces. 
 * Using NRCLex on each portion to get sentiment scores 
This yields a 10x12=120 dimensional sentiment vector for each movie transcript. Using only this portion as the feature matrix, I used a randomforest to predict the scores.
### Visualization
I used wordcloud and matplotlib to generate the following plots for a given movie:
 * A cumulative sentiment evolution 

<p align="center">
  <img width="680" height="350" src="https://raw.githubusercontent.com/kcandost/TDI_Capstone/master/img/Joker_total_sentiment.jpg">
</p>

* A wordcloud

<p align="center">
  <img width="680" height="350" src="https://raw.githubusercontent.com/kcandost/TDI_Capstone/master/img/Joker_wordcloud.jpg">
</p>
 
 * A radar chart 

<p align="center">
  <img width="460" height="460" src="https://raw.githubusercontent.com/kcandost/TDI_Capstone/master/img/Joker_radar.jpg">
</p>
 
<div align="center">

| Movie      | Anger | Negative | Trust | Anticipation | Joy  | Positive | Fear | Sadness | Surprise | Disgust 
|------------|-------|----------|-------|--------------|------|----------|------|---------|----------|---------|
| Joker      | 365   | 897      | 661   | 614          | 1388 | 1823     | 452  | 540     | 1169     | 275     | 

</div>
 
<div align="center">

| Year | Score |          Genre           |   
|------|-------|--------------------------| 
|2019  | 8.4   | [Crime, Drama, Thriller] | 

</div>

### Discussion
When we use sentiment scores of individual portions of transcript to construct the feature matrix, the model yields a low score of $R^2\approx 0.01$. In an attempt to be able to explain more of the variation, I also tried to construct the feature matrix using the cumulative sentiment scores, which yielded $R^2\approx 0.03$. Therefore it is safe to say that sentiment evolution alone does not provide a strong enough signal for predicting movie scores.

There are many other factors that effect the success of a movie that cannot be captured via the transcript alone, a few of which are: actors, visuals, soundtracks, and the delivery. Although it is possible to improve the model by including the categorical features to the pipeline, the result remains the same: The sentiment evolution of a movie transcript is not a viable metric to predict its success. 

---
This project was developped during my scholarship at The Data Incubator.

