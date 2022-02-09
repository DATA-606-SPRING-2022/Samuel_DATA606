# The Fear-Industrial Complex<sup>1</sup>
*An analysis on the amount of fear that plays into current US news media by Samuel Kolodrubetz*

## Topic Introduction and Questions to Answer

Anyone somewhat familiar with journalism and/or news media knows the quote "if it bleeds, it leads"<sup>2</sup>. For those who aren't, this essentially tells us that popular and leading stories often involve blood, death, or controversial subjects. While this theme has been around since the late 19<sup>th</sup> century, this way of thinking still rings true. Turn on any local TV station, and its highly likely that the top story will involve violence, scandals, or something similar. One thing is common in many of these leading stories: fear. Fear is one of the most common ways news outlets generate clicks/reads and ensure the audience comes back and continues reading. As The Hill states: "The news agenda on a micro level covers a variety of dreadful events and stories, but the macro message boils down to one headline: 'Be Afraid.'"<sup>3</sup>. For my capstone project, I am attempting to look into the question of fear-based media. Using Natural Language Processing (specifically sentiment analysis), I will attempt to address two questions: 

1. First, is fear-based journalism still prevalent in the 2020s in a particular news topic (politics, finance, pop culture, etc.)? And next, 
2. Is there a difference in the amount of fear used for different large media outlets? 

## Data Source and Description

In order to classify an article as fearful, or any other emotion, we first need to create a model that is able to determine the intended emotion of a sentence or article. this data comes from [huggingface.co](https://huggingface.co/datasets/emotion), which contains sentences that are labeled for 5 emotions: sadness, joy, love, anger, and fear. The dataset contains 20,000 labeled sentences with a 80%/10%/10% split between train/validation/test. 

**Note:** This dataset is similar to [one found on Kaggle](https://www.kaggle.com/pashupatigupta/emotion-detection-from-text), but that dataset focuses on tweets with emotion where this dataset is simply sentences. [Huggingface dataset github](https://github.com/dair-ai/emotion_dataset)

Once the model(s) is trained and tested to a sufficient accuracy, I am then able to perform the analysis of emotions being used on real-world articles. To do this, I first need to get the articles' text from various news outlets on the internet through a web scraping. In order to determine how fear and other emotions are used differently in different outlets, I will be considering three news outlets across the political spectrum: AP News, CNN, and Fox News. Additionally, since the style of reporting for different topics (politics, world news, finance, etc.) differs I am going to choose only one of these topics to scrape the articles from to remain consistent. I have not currently chosen the specific topic, but I am leaning towards finance. For this kind of project where we are using text to analyze feelings of articles the more data gathered is always better to capture trends and find the outliers. Once the model is trained to a reasonable accuracy, testing will not require much time or computing power (I plan on using the same preprocessing steps for the articles as the training data where appropriate to maintain a similar input format for both steps) since it is essentially just a prediction being made using the model. Therefore, to start I will take around 50 articles from each outlet, with the possiblity of adding more if everything goes well. 

Next, the variable of measure in this project is the emotion of the article/headline/sentence. While the main focus will be on the negative emotions of fear and anger, having a way to quantify other emotions could prove beneficial to the final outcome. With that, I can quantify the level of each emotion being shown within each article. For each article, the intended output will be a list of probabilities that the given input (article/sentence) belongs to each class (emotion). For example, a sentence reading "I am feeling sad" could have an output of (0.98, 0, 0, 0.01, 0.01), where the first value is the "saddness" class meaning the model predicts that sentence is showing sadness with a high probability. This is the baseline of measuring fear within each article, in what I will call the "Fear Index". The higher the probability the model gives to the "fear" class, the higher the Fear Index. Additionally, for measuring the relative use of fear across various news outlets, I will take into account each outlet's number of articles and the individual article's Fear Index. 

## Methodologies

This project will involve several steps that will utilize various techniques of a data science project:

1. Model Creation - Before quantifying the amount of fear in real-world articles, we need to train a model for sentiment analysis on our labeled emotion text data. To do this, I am going to be using Deep Learning. One of the most common models is a Recurrent Neural Network (RNN), which make processing sequences of data (sentences or articles) more effective. Because of my experience with it over other Deep Learning Python libraries, I will likely be using PyTorch and its associated packages. 
2. Data Scraping - As mentioned above, the individual data "entries" are going to be the individual articles pulled from the various news sites. This will be done using a Python library (either Scrapy, Beautifulsoup, or Selenium)
3. Data Cleaning - Preprocessing the incoming articles is incredibly important; text data needs to be put into a format that a machine can actually work with. Some important parts of this process are tokenization (breaking the article/sentence down into the simplest format for the machine to work with), stemming (finding the root of a given word, i.e from "eats" to "eat"), and removing unimportant "stop words" (words such as "the" or "and" which hold no value in NLP). This preprocessing will be done both for the model creation step and when analyzing the real-world articles.  

## Intended Outcomes

Language is subjective; knowing what a writer/speaker intends to say when they write “shut up” takes context and understanding for the audience to know what they mean. Because of this, I do not fully expect a completely successful classification of articles as fearful. However, a baseline result I expect is to have a well-performing model on a set of heavily curated articles that are chosen specifically for using fearful language throughout. For example, an article with the name “Cute Dog and Cute Cat Cuddle” would be expected to be very positive and not full of fear, while an article titled “World Ending in Less than a Year” would be regarded as a very negative article. The baseline outcome I expect is the first article to be very low on the Fear Index (0) with the latter being scored very high. 

For comparison across the various news outlets, I expect one main outcome: sites like AP News tend to sensationalize articles and headlines less than sites with political leanings like CNN and Fox News, so I would expect the overall fear level being used with AP News to be less than the other two. The other sites will, in my opinion be subjective to the articles that are actually scraped, but I would expect them to be relatively similar.


## Sources
<sup>1</sup> - https://abcnews.go.com/2020/story?id=2898636&page=1 - An ABC News article about how fear is a big factor in the stories that are followed, and the ones that ultimately find success. This article is the inspiration for this project's title.  
<sup>2</sup> - https://www.chicagotribune.com/news/ct-xpm-1989-11-05-8901280504-story.html - the first known appearance of the phrase "if it bleeds, it leads" comes from a New York Magazine article titled "Grins, Gore, and Videotape" by Eric Pooley. This Chicago Tribune article by Eleanor Randolph notes, this as I was unable to find the original article.

<sup>3</sup> - https://thehill.com/opinion/technology/556160-media-spread-fear-americans-listen


