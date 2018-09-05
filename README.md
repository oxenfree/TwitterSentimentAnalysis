# TwitterSentimentAnalysis
## SETUP 

In the same directory as this script, you'll need
a file called 'config.py'. In that file, you'll 
need to put your twitter authentication credentials. 
Such as:
consumer_key = '_your_twitter_key_'
consumer_secret = '_your_twitter_secret_'
access_token = '_your_token_'
access_token_secret = '_your_token_secret_'
These are imported at the top of this script and are required
for the script to run correctly.
## USAGE

1) Pick a search phrase to pull tweets from twitter:
search_phrase = '#abcxyz' # change this to the search phrase
2)  Set a search limit, the total number of tweets to 
    pull in. Keep in mind twitter has a daily limit on 
    API calls:
 
tweet_limit = 3  # change this to the number of tweets you want
3) Make a new TweetHandler, like this:
handler = TweetHandler()
4) Pull tweets with your search phrase and size limit:
tweets = handler.get_tweet_attributes_map(search_phrase, tweet_limit)
5)  Optional: you can take out the 'RT' and '@' symbols 
    from the tweet texts.
    
clean = handler.clean_tweet_map_texts(tweets)
6) Optional: get the nltk_sentiment scores for each tweet:
sent_map = handler.add_nltk_sentiment_map(clean)
7)  Optional: geth the TextBlob sentiment score for each tweet.
    TextBlob ranks phrases by -1, 0, 1 (-1: negative, 0: neutral, 1: positive)
sent_map = handler.add_text_blob_sentiment_map(sent_map)
8)  Optional: stem the tweet texts. Stemming can change the meaning
    and sentiment of a phrase though.
stems = handler.stem_tweet_texts(cleaned_tweets)
## DATA

You will now have a number of tweets with a datetime, text,
device (such as "Android" or "iPhone" or "Web"), and optionally 
you can have stemmed or sentiment analyzed texts for each tweet. 
The tweet dictionary structure is like:
{
    0: {
        date: datetime.datetime(2018, 8, 30, 19, 24, 47),
        'device': 'Twitter for Android',
        'text': "As resident of AndrewGillum's Tallahassee...',
        'nltk_pos': 0.26249691321696916,
        'nltk_neu': 0.8573198090476511,
        'nltk_neg': 0.7375030867830308,
        'blob_sent': -1
    },
    1: {
        'date': datetime.datetime(2018, 8, 30, 19, 24, 6),
        'device': 'Twitter for Android',
        'text': ' ScottPresler: The socialist and democrat ...',
        'nltk_pos': 0.592341302535156,
        'nltk_neu': 0.8948539758194366,
        'nltk_neg': 0.40765869746484396,
        'blob_sent': 0
    }
}
Note: This example shows unstemmed tweets. Stemmed tweets will have the same
structure, but the text will be stemmed.
