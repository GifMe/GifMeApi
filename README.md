GifMeApi
========

GifMe is an app that makes saving, sharing and organizing gifs easier. It is also home to one of the largest gif search engines. GifMe has an API that allows 3rd party developers to use the data and tap into the gifs and images collected by GifMe users.

## Basics
The API is a read only api. You can query a number of endpoints and get data from those. Below is the documentation on how to use it.

## Search
The search API is powered by the same engine and alogrithm that powers the GifMe search engine. It accepts a query and will first find all tags that contain the query, then run an algorithm that scores the tags agains the query and produces a 'score'. The lower the score the more relavent the tag is to the query.

<b>Endpoint</b>: `http://api.gifme.io/v1/search`
