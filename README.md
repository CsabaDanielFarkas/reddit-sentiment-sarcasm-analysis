# Reddit Sentiment and Sarcasm Analysis
## Goals
Evaluate using a barchart, what the community thinks of a post according to the comments.
Our input is a Reddit link, output is a barchart.
## Problems
1. Collecting the data - this task is easily handled with PRAW - Python Reddit API Wrapper.
2. Sarcastic comments, irony and other figures of speech add a huge layer of problems.
-"*Holy shit. This is incredible. I’m embarrassed now I have love handles and I was complaining about having to exercise*" - Under a weight loss progression post. Naturally, the comments are mostly positive congratulating the poster. This comment itself has a positive message, but the word "embarassment" has a negative connotation. Most Sentiment algorithms capture it as an indicator, that the comment is negative, which it is certainly not.

Such figures will stay a problem, but a very satisfying solution is bringing a sarcasm detector into play and using it with the sentiment analysis together:
<p align="center" width="100%">
    <img width="50%" src="https://github.com/CsabaDanielFarkas/reddit-sentiment-sarcasm-analysis/blob/main/Images/sarcasm_table.PNG">
</p>

Swapping values when irony is detected. At the end, we will demonstrate, that this indeed makes our predictions more precise - which actually proves, that sarcastic speech is incredibly frequent on Reddit.

3. Choosing a good algorithm for sentiment analysis

## VADER v Flair v TextBlob
All three yielded pretty good results, all of them had their pros and cons. Mainly the training set and the algorithms themselves.
TextBlob and VADER weren't much different. VADER itself is well fit for social media, but it is uses a lexical approach - it doesn't use any ML algorithms. That is no problem though. Flair on the other hand was pre-trained on an IMDB dataset, which is quite different from social media, but it still did well. In a notable case "Jake beat cancer", which is a positive message, VADER yielded NEGATIVE, since both words "beat" and "cancer" are very negative. On the other hand, Flair yielded a POSITIVE message. Thus, very impressed by Flair, I decided to use it. 

## Sarcasm detection
I pre-trained a sarcasm detector using the "Sarcastic Headlines Dataset" - available on Kaggle. First step was to vectorize the words using the TfidfVectorizer, then later training it with a LinearSVC model. The model worked with minor flaws.

# Final results
- Weight loss journey: https://www.reddit.com/r/progresspics/comments/g0h7wm/m3168_764lbs_299lbs_465lbs_update_6_finally_under/

<p align="center" width="100%">
    <img width="50%" src="https://github.com/CsabaDanielFarkas/reddit-sentiment-sarcasm-analysis/blob/main/Images/WeightLoss.jpg">
</p>

- Abortion ban news: https://www.reddit.com/r/news/comments/vjpfbh/supreme_court_overturns_roe_v_wade_states_can_ban/
<p align="center" width="100%">
    <img width="50%" src="https://github.com/CsabaDanielFarkas/reddit-sentiment-sarcasm-analysis/blob/main/Images/AbortionBan.jpg">
</p>

By both cases, Flair does a great job, the sentiment analysis almost makes no changes. When Flair reads posts with mostly 50/50, that's when the sarcasm detector shines the most. It almost always pushes the stats towards the right answer! It is still up to the user to analyze the findings themselves, since the human language really is cryptic. 
