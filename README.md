<p align="center">
  <img src="https://github.com/iamcalebjones/WallStreetBots/blob/main/images/bots2.png">
  <figcaption>Source www.ingridhusby.com</figcaption>
</p>

# r/WallStreetBots
## Investigating whether or not bots contributed to the hype that helped drive up the price of GameStop stock in early 2021.
#### By Caleb Jones
[LinkedIn](https://www.linkedin.com/in/calebsjones/) | [GitHub](https://github.com/iamcalebjones) | [Presentation Slides](link-coming-later)

## Background

Reddit is a place on the internet. [Wikipedia](https://en.wikipedia.org/wiki/Reddit) states it is "a social news aggregation, web content rating, and discussion website" which is grouped into pages called subreddits, or subs, which contain topic-specific content. Reddit users can join specific subs to participate in that community's discussion.

One particular subreddit, called [r/WallStreetBets](https://www.reddit.com/r/wallstreetbets/), exists to discuss stock and options trading. For the last year or so, members there have been speculating about the value of GameStop (GME) stocks. GameStop is a chain of brick and mortar stores that sells consumer electronics and gaming merchandise. Over the last few years, the company has been in decline due to the popularity of games being bought and sold online, and combined with the pandemic and struggle that brought to physical stores, GME was in bad shape. Such bad shape that hedge fund managers took large short positions on the stock, betting the value would continue to decrease, which would make them money. Hedge fung managers were so commmitted to this strategy that the stock was over 100% shorted. Members of r/WallStreetBets noticed this high short interest ratio, and GME became a frequent topic of discussion on the sup.

## Natural Language Processing

To evaluate this subject, I needed data. At first, I thought it would take a lot of scraping or navigating with the Reddit API to obtain the information, but as it turns out, this topic is suddenly very popular, and someone had already done the legwork and posted it to [Kaggle](https://www.kaggle.com/mattpodolak/rwallstreetbets-posts-and-comments). 

Armed with data, I proceeded with the workflow common to text processing known as Natural Language Processing, or NLP. This usually includes removing unnecessary text like links if they are present, normalizing all the various forms of words into single root word format so that they can be analyzed as a single term, removing stop words, and usually constructing n-grams, which are series of words as they appear in the original text, to help retain context.

In this case, I did have to remove links, and I also removed numbers from the text as well. This is 
