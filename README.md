<p align="center">
  <img src="https://github.com/iamcalebjones/WallStreetBots/blob/main/images/bots2.png">
  <figcaption>Source www.ingridhusby.com</figcaption>
</p>

# r/WallStreetBots
## This is a natural language study of the subreddit r/WallStreetBets as it relates to the surge in the stock price of GameStop, and investigates whether or not bots contributed to the hype that helped drive up the stock's price in early 2021.
#### By Caleb Jones
[LinkedIn](https://www.linkedin.com/in/calebsjones/) | [GitHub](https://github.com/iamcalebjones) | [Presentation Slides](https://www.beautiful.ai/player/-MXUgJDSZlYIPIvNQRGx)

## Background

Reddit is a place on the internet. [Wikipedia](https://en.wikipedia.org/wiki/Reddit) states it is "a social news aggregation, web content rating, and discussion website" which is grouped into pages called subreddits, or subs, which contain topic-specific content. Reddit users can join specific subs to participate in that community's discussion.

One particular subreddit, called [r/WallStreetBets](https://www.reddit.com/r/wallstreetbets/), exists to discuss stock and options trading. For the last year or so, members there have been speculating about the value of GameStop (GME) stocks. GameStop is a chain of brick and mortar stores that sells consumer electronics and gaming merchandise. Over the last few years, the company has been in decline due to the popularity of games being bought and sold online, and combined with the pandemic and struggle that brought to physical stores, GME was in bad shape. Such bad shape that hedge fund managers took large short positions on the stock, betting the value would continue to decrease, which would make them money. Hedge fung managers were so commmitted to this strategy that the stock was over 100% shorted. Members of r/WallStreetBets noticed this high short interest ratio in early 2020, and GME became a frequent topic of discussion on the sub. 

The plot below shows both the GME stock ticker price and the posts contributed to r/WallStreetBets on a daily basis, and the relationship between the two is strikingly similar.

<p align="center">
  <img src="https://github.com/iamcalebjones/WallStreetBots/blob/main/images/dual_plot.png">
</p>

Here are a few details about these two trends:

  - Between December 14th and January 12th, the average price of GME was $18.55 per share
  - Over the same time period, r/WallStreetBets averaged 275 posts per day
  - GME hit its peak on January 28th, at $483 per share
  - r/WallStreetBets also saw its peak daily posts contributed on January 28th, 28119 individual posts



## Natural Language Processing

As far as data is concerned, at first I thought it would take a lot of scraping or navigating with the Reddit API to obtain the information, but as it turns out, this topic is suddenly very popular, and someone had already done the legwork and posted it to [Kaggle](https://www.kaggle.com/mattpodolak/rwallstreetbets-posts-and-comments). 

I more or less followed the usual steps associated with Natural Language Processing, or NLP. My workflow consisted of removing line breaks, apostrophes, hyperlinks, special characters, and finally numbers. I chose to just remove apostrophes from the contractions instead of expanding them on my first pass through the data, and I felt that the quality of the processed data didn't suffer as a result of this decision. 

A big task with this dataset was handling emojis, because the contributors to r/WallStreetBets frequently use them and they were everywhere in the dataset. What I came up with was a method to translate them to their word descriptions, and adding the word 'emoji-' to the beginning. For example, 🚀&nbsp; is the rocket, but just translating this symbol to 'rocket' would not preserve information that it was initially an emoji, so in my dataset, this became 'emojirocket'. This actually worked pretty well, and in my modeling it was very easy to identify the emojis later on.

Next I lemmatized words, and finally removed stop words. Originally I wanted to also include n-grams to preserve some information about word usage and context, but the size of the dataset was prohibitive. The resulting dataset was too large, both in RAM space and in processing/modeling time, so I proceeded with just single words. 

## Modeling

