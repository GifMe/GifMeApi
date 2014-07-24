GifMeApi
========

<img src='http://gifme.io/powered_by.png' />

GifMe is an app that makes saving, sharing and organizing gifs easier. It is also home to one of the largest gif search engines. GifMe has an API that allows 3rd party developers to use the data and tap into the gifs and images collected by GifMe users.

## Basics
The API is a read only api. You can query a number of endpoints and get data from those. Below is the documentation on how to use it. You can query these enpoints as basic GET requests.

## API KEY
For the time being you are free to use the following key. Please note that any abuse of this key will result in a change of policy. We are working to setup a dev center where you can register to get a key for your app.

If you plan to use the API in a production application please email us hello@gifme.io and we can set you up with a specific key.

## POWERED BY TAGS
There are a number of powered by tags that you can use.

<img src='http://gifme.io/powered_by.png' /><br/>
`http://gifme.io/powered_by.png`

<img src='http://gifme.io/powered_by_white.png' /><br/>
`http://gifme.io/powered_by_white.png`

<img src='http://gifme.io/powered_by_black.png' /><br/>
`http://gifme.io/powered_by_black.png`

<img src='http://gifme.io/powered_by_black_out.png' /><br/>
`http://gifme.io/powered_by_black_out.png`

<b>API KEY</b>: `rX7kbMzkGu7WJwvG`

## Search
The search API is powered by the same engine and alogrithm that powers the GifMe search engine. It accepts a query and will first find all tags that contain the query, then run an algorithm that scores the tags agains the query and produces a 'score'. The lower the score the more relavent the tag is to the query.

<b>Endpoint</b>: `http://api.gifme.io/v1/search`
<b>Arguments</b>
<ul>
	<li><b>query</b> - The term you are searching for </li>
	<li><b>limit</b> - The number of results to serve up. Max 42</li>
	<li><b>page</b> - The page of results you want <b>NOTE: Pages are 0 based</b></li>
	<li><b>sfw</b> - true or false, will filter NSFW Gifs</li>
	<li><b>key</b> - Your API key</li>
</ul>

Upon hitting the API you will get a response that looks similar to this:

<pre>
{
	status: 200,
	meta: {
		term: "r/filmgifs",
		limit: 1,
		page: 0,
		total_pages: 52,
		total: 52,
		timing: "0.167ms"
	},
	data: [
		{
			id: 162445,
			score: 0,
			nsfw: false,
			link: "http://i.imgur.com/FkQ1Hfv.gif",
			thumb: "http://i.gifme.io/gifme/thumb__1e656c194f.gif",
			created_at: "2014-07-14T22:28:27.412Z",
			tags: [
				"fast",
				"times",
				"ridgemont",
				"high",
				"skull",
				"shoe",
				"weed",
				"smoke",
				"420",
				"pot",
				"bong",
				"phone",
				"loop",
				"cinemagraph",
				"r/filmgifs"
			]
		}
	]
}
</pre>

This query was `http://api.gifme.io/v1/search?query=r/filmgifs&limit=1&page=0&key=rX7kbMzkGu7WJwvG`

From the results you will see the following:
<ul>
	<li><b>Status</b>: The server status</li>
	<li><b>Meta</b>
		<ul>
			<li><b>Term</b>: The term you searched for.</li>
			<li><b>limit</b>: Number of results you requested.</li>
			<li><b>page</b>: Current page of results you requested.</li>
			<li><b>total_pages</b>: Total number of pages based on your limit.</li>
			<li><b>total</b>: Total number of results.</li>
			<li><b>timing</b>: Time it took to process in ms.</li>
		</ul>
	</li>
	<li><b>Data</b>
		<ul>
			<li><b>id</b>: Gif ID</li>
			<li><b>score</b>: The relevancy to your term ( 0 is best )</li>
			<li><b>nsfw</b>: If the result is NSFW</li>
			<li><b>link</b>: The original source</li>
			<li><b>thumb</b>: The static thumbnail</li>
			<li><b>created_at</b>: Creation date</li>
			<li><b>Tags</b>: The other tags associated with this Gif</li>
		</ul>
	</li>
</ul>

<b>NOTE: Pages are 0 based</b> This means that page 0 is the first page.


## Stream
The stream is a real time stream of Gifs and tags that are saved into GifMe. 

<b>Endpoint</b>: `http://api.gifme.io/v1/stream?key=rX7kbMzkGu7WJwvG`

The results of this query will look something like this:

<pre>
{
	status: 200,
	meta: {
		timing: "0.521ms"
	},
	data: [
		{
			id: 481585,
			created_at: "2014-07-20T03:54:10.844Z",
			thumb: "http://i.gifme.io/gifme/thumb__6b3c891d38.gif",
			link: "http://i.imgur.com/fB19z.gif",
			nsfw: false,
			tags: [
				"over your head"
			]
		},
		{
			id: 481584,
			created_at: "2014-07-20T03:53:48.245Z",
			thumb: "http://i.gifme.io/gifme/thumb__1c019b1953.gif",
			link: "https://31.media.tumblr.com/7ac1def41e60d8c1c75c9a1638a1a4ec/tumblr_n8vnk0tD4V1s95j2so5_250.gif",
			nsfw: false,
			tags: [
				"but we arnt men"
			]
		}
	]
}
</pre>

Similar to the search return. Note that the tags are returned as a string and not broken up.

<ul>
	<li><b>Status</b>: The server status</li>
	<li><b>Meta</b>
		<ul>
			<li><b>timing</b>: Time it took to process in ms.</li>
		</ul>
	</li>
	<li><b>Data</b>
		<ul>
			<li><b>id</b>: Gif ID</li>
			<li><b>nsfw</b>: If the result is NSFW</li>
			<li><b>link</b>: The original source</li>
			<li><b>thumb</b>: The static thumbnail</li>
			<li><b>created_at</b>: Creation date</li>
			<li><b>Tags</b>: The other tags associated with this Gif</li>
		</ul>
	</li>
</ul>

There are more enpoints on the way and we will be publishing them here as well as more documentation on the site.
