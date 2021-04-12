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

One particular subreddit called [r/WallStreetBets](https://www.reddit.com/r/wallstreetbets/), exists to discuss stock and options trading. For the last year or so, members there have been speculating about the value of GameStop (GME) stocks. GameStop is a chain of brick and mortar stores that sells consumer electronics and gaming merchandise. Over the last few years, the company has been in decline due to the popularity of games being bought and sold online, and combined with the pandemic and struggle that brought to physical stores, GME was in bad shape. Such bad shape that hedge fund managers took large short positions on the stock, betting the value would continue to decrease, which would make them money. Hedge fung managers were so commmitted to this strategy that the stock was over 100% shorted. Members of r/WallStreetBets noticed this high short interest ratio in early 2020, and GME became a frequent topic of discussion on the sub. 

The plot below shows both the GME stock ticker price and the posts contributed to r/WallStreetBets on a daily basis, and the relationship between the two is strikingly similar.

<p align="center">
  <img src="https://github.com/iamcalebjones/WallStreetBots/blob/main/images/dual_plot.png">
</p>

Here are a few details about these two trends:

  - Between December 14th and January 12th, the average price of GME was $18.55 per share
  - Over the same time period, r/WallStreetBets averaged 275 posts per day
  - GME hit its peak on January 28th, at $483 per share
  - r/WallStreetBets also saw its peak daily posts contributed on January 28th, 28119 individual posts

Focusing on January 28th for a moment, there was a particularly high occurence of emojis, The following emojis showed up the most on this day:

  - 🚀&nbsp; had 4476 uses
  - 💎&nbsp; had 200 uses
  - 🦍&nbsp; had 100 uses
  - 🙌&nbsp; had 73 uses

A typical post incorporating emojis looks like "To the moon!!! 🚀🚀🚀🚀🚀🚀🚀🚀🚀&nbsp; we have 💎💎💎🙌!" The 💎💎💎🙌 emoji combination is known as 'diamond hands' which users who were holding shares of GME said in reference to holding stocks that were suddenly so valuable. "To the moon" was said in reference to users wanting to see the stock continue to rise, and many believe $1,000 per share was possible. 

Although the stock hasn't reached that price, several frequent contributors to the subreddit managed to make massive money on January 28th. Mike McCaskill held 750 $60 call options which he exited at a price of $347 per share and walked away with $25 million. Reddit user u/DeepF\*ckingValue, who's YouTube name is Roaring Kitty and goes by Keith Gill when not on the internet, had been posting to r/WallStreetBets nearly daily for several weeks with screenshots of his brokerage account and the value that he had amassed. At his peak, he was worth $47 million, but he didn't sell, a true 💎💎💎🙌. In reality, most of his value was due to the long-term options positions he had opened, which expire on April 12th. He's going to wait as long as possible to exercise his options in the hope that the price is as high as possible before he exits.

## Natural Language Processing

As far as data is concerned, at first I thought it would take a lot of web scraping or navigating the Reddit API to obtain the information, but as it turns out, this topic is suddenly very popular, and someone had already done the legwork and posted it to [Kaggle](https://www.kaggle.com/mattpodolak/rwallstreetbets-posts-and-comments). The provided data was broken into posts and comments, and the datasets were 915 mb and 3.39 gb, respectively. Because of the size of the datasets, I started off working with the posts data.

I generally followed the standard steps associated with Natural Language Processing, or NLP. My workflow consisted of removing line breaks, apostrophes, hyperlinks, special characters, and finally numbers. I chose to just remove apostrophes from the contractions instead of expanding them on my first pass through the data, and I felt that the quality of the processed data didn't suffer as a result of this decision. 

A big task with this dataset was handling emojis, because the contributors to r/WallStreetBets frequently use them and they were everywhere in the dataset. What I came up with was a method to translate them to their word descriptions, and adding the word 'emoji-' to the beginning. For example, 🚀&nbsp; is the emoji named 'rocket', but just translating this symbol to 'rocket' would not preserve information that it was originally an emoji, so in my dataset this became 'emojirocket'. This actually worked very well, and in my modeling it was very easy to identify the emojis later on.

Next I lemmatized words, and finally removed stop words. I'd planned on using n-grams to preserve some information about word usage and context, but the size of the dataset was prohibitive. The resulting dataset was too large, both in RAM space and in processing/modeling time, so I proceeded with just single words. 

## Modeling

After running my data through the processing steps outlined above, I first built a WordCloud for the sake of the visual. The WordCloud shows the payoff of the previously outlined emoji translation efforts, as it is very easy to see the presence of emojis. Several standouts present here are the emojis for rocket, gemstone, eggplant, and raising hands (the character in 'diamond hands'). Looking a little closer, **the bots have identified themselves aboard the rocket emoji**, right between the 'i' and 'r', surely riding this stock to the moon.

<p align="center">
  <img src="https://github.com/iamcalebjones/WallStreetBots/blob/main/images/comments_wordcloud.png">
</p>

I then ran the processed text data through a clustering model. My theory was that if bots were regularly conributing to the sub and hyping GME to drive up the price, their posts would be evident in a clustering model. I expected that the posts would cluster into 3 groups: humans, bots, and other (or 'unable to tell if human or bot'). I ran a KMeans clustering model with it constrained to 3 clusters
