# Reddit Sentiment and Sarcasm Analysis
## Goals
Evaluate using a barchart, what the community thinks of a post according to the comments.
Our input is a Reddit link, output is a barchart.
## Problems
1. Collecting the data - this task is easily handled with PRAW - Python Reddit API Wrapper.
2. Sarcastic comments, irony and other figures of speech add a huge layer of problems.
-"*Holy shit. This is incredible. I’m embarrassed now I have love handles and I was complaining about having to exercise*" - Under a weight loss progression post. Naturally, the comments are mostly positive congratulating the poster. This comment itself has a positive message, but the word "embarassment" has a negative connotation. Most Sentiment algorithms capture it as an indicator, that the comment is negative, which it is certainly not.

Such figures will stay a problem, but a very satisfying solution is bringing a sarcasm detector into play and using it with the sentiment analysis together:
