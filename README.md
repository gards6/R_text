# R_Text
# script from https://www.youtube.com/watch?v=JoArGkOpeU0 Jalayer Academy
text mining with R 

install.packages("twitteR")
install.packages("RCurl")

require(twitteR)
require(RCurl)

consumer_key <- ‘’
consumer_secret <- ‘’
access_token <- ‘’
access_secret <- ‘’

setup_twitter_oauth(consumer_key, consumer_secret, access_token, access_secret)

Car_Tweets <- searchTwitter("car",n=10, lang="en")
Car_Tweets

install.packages(“tm/ wordcloud”)


require(tm)
require(wordcloud)

worldcup <- searchTwitter('world+cup', lang="en", n=500, resultType = "recent")
class(worldcup)
worldcup_text <- sapply(worldcup, function(x) x$getText() )

str(worldcup_text)


** create corpus (text file) of tweets  **

cup_corpus <- Corpus(VectorSource(worldcup_text))
cup_corpus

** look at first document within the corpus **
inspect(cup_corpus[1])

** lowercase, remove numbers, remove whitespace, remove punctuation **
cup_clean <- tm_map(cup_corpus, removePunctuation)
cup_clean <- tm_map(cup_corpus, content_transformer(to lower)
cup_clean <- tm_map(cup_corpus, removeWords, stopwords(“english”))
cup_clean <- tm_map(cup_corpus, removeNumbers)
cup_clean <- tm_map(cup_corpus, stripWhitespace)

** you can remove search words that will obviously appear in tweets **
cup_clean <- tm_map(cup_clean, remove words, c(“soccer”, “world”, “cup”))

** generate wordcloud and tweak parameters as desired **

wordcloud(cup_clean)

wordcloud(cup_clean, random.order=F, max.words=40, scale=c(3, 0, 5), colors=rainbow(50)







