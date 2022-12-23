# Stock Market & Financial News API

Access stock market and financial news of all publicly traded companies listed on US stock exchanges.

- More than 50 million articles accessible
- All major newswires included
- Real-time news stream API and historical news search API 

Get your free API key: https://newsfilter.io/api-plans

# Installation

```bash
pip install financial-news-api
```

# Search API

The Search API allows you to access and search the news database with over 50 million articles. 
Newly published articles are added in real-time to the database.

```python
import requests

API_KEY = "YOUR_API_KEY"
API_ENDPOINT = "https://api.newsfilter.io/search?token={}".format(API_KEY)

# Define the news search parameters
queryString = "symbols:NFLX AND publishedAt:[2020-02-01 TO 2020-05-20]"

payload = {
    "queryString": queryString,
    "from": 0,
    "size": 10
}

# Send the search query to the Search API
response = requests.post(API_ENDPOINT, json=payload)

# Read the response
articles = response.json()

print(articles)
```

### Example Response

```json
{
  "articles": [
    {
      "title": "FAANG emerges as the latest group to lead the market, Jim Cramer says", 
      "description": "\"This market's been going through leadership groups like there's no tomorrow,\" the \"Mad Money\" host said.",
      "publishedAt": "2020-05-20T22:32:22+0000",
      "sourceUrl": "https://www.cnbc.com/2020/05/20/faang-emerges-as-the-latest-group-to-lead-the-market-jim-cramer-says.html",
      "source": {
        "name": "CNBC",
        "id": "cnbc"
      },
      "symbols": [
        "FB",
        "AAPL",
        "AMZN",
        "NFLX",
        "GOOGL",
        "TGT",
        "WMT",
        "HD",
        "LOW"
      ],
      "sectors": [
        "Technology",
        "Consumer Cyclical",
        "Consumer Defensive"
      ],
      "industries": [
        "Internet Content & Information",
        "Consumer Electronics",
        "Specialty Retail",
        "Media - Diversified",
        "Discount Stores",
        "Home Improvement Stores"
      ],
      "imageUrl": "https://image.cnbcfm.com/api/v1/image/103267851-IMG_0161.jpg?v=1545882603",
      "id": "01a030ca440ba8732461703e9a906eb7"
    },
    {
      "title": "S&P 500 Clawing Toward 3,000 Milestone Finds Road Getting Harder",
      "description": "A rally this week has pushed the S&amp;P 500 Index to 2,972. The 28-point road to 3,000 could be a slog.",
      "publishedAt": "2020-05-20T20:18:32.731Z",
      "sourceUrl": "https://www.bloomberg.com/news/articles/2020-05-20/s-p-500-s-next-even-number-milestone-will-be-tough-to-reach",
      "source": {
        "name": "Bloomberg",
        "id": "bloomberg"
      },
      "symbols": [
        "FB",
        "AMZN",
        "NFLX"
      ],
      "sectors": [
        "Technology",
        "Consumer Cyclical"
      ],
       "industries": [
        "Internet Content & Information",
        "Specialty Retail",
        "Media - Diversified"
      ],
      "imageUrl": "https://assets.bwbx.io/images/users/iqjWHBFdfxIU/iiT4fbpCD7v8/v2/-1x-1.png",
      "id": "a63b37b42f4c2a856535a3b7e8bb3190"
    }
  ]
}
```

# Stream API

Setting up a news streaming API to receive newly published articles in real-time can be done in less than 10 lines of code.

First, install `socket.io` for Python:

```
pip install python-engineio==3.14.2 python-socketio[client]==4.6.0
```

> Please use the exact `python-engineio` and `python-socketio` versions above.

The example below creates a `socket.io` client, connects to the Stream API server and prints new articles as they are published.

```python
import socketio

sio = socketio.Client()

@sio.on('connect')
def on_connect():
    print("Connected to Newsfilter Stream API")

@sio.on('articles')
def on_articles(articles):
    print(articles)

sio.connect('http://stream.newsfilter.io?apiKey=YOUR_API_KEY')
sio.wait()
```

# Topics

The news API supports a large range of topics, for example:
- Quarterly and annual earnings reports
- Insider trading reports filed with the SEC
- Merger & acquisition news
- IPOs and offerings
- Legal proceedings and federal investigations
- Changes to management

# News Sources


| News Provider                  |                                 Source ID |
|--------------------------------|------------------------------------------:|
| Analyst Ratings                |                           analystUpgrades |
| Bloomberg                      |                                 bloomberg |
| Reuters                        |                                   reuters |
| CNBC                           |                                      cnbc |
| Wall Street Journal            |                       wall-street-journal |
| Barrons                        |                                   barrons |
| PR Newswire                    |                                prNewswire |
| Globe Newswire                 |                             globenewswire |
| BusinessWire                   |                              businesswire |
| AccessWire                     |                                accesswire |
| SeekingAlpha                   |                              seekingAlpha |
| Zacks Equity Research          |                                     zacks |
| Benzinga                       |                                  benzinga |
| S&P Global                     |                               sandpGlobal |
| Earnings Call Transcripts      |                   earningsCallTranscripts |
| **US:**                        |                                           |
| ClinicalTrials.gov             |                            clinicaltrials |
| Gov. Contract Awards (SAM.gov) |                                     usSam |
| SEC Filings                    |                                   sec-api |
| SEC Press Releases             |                          secPressReleases |
| FCC Filings                    |                                fccFilings |
| CFTC Press Releases            |                                      cftc |
| Patent Database (USPTO)        |                                     uspto |
| Patent Trial & Appeal Board    |                       usptoTrialAndAppeal |
| Department of Defense          |                                     usDod |
| FDA Drug Approvals             |      usFda (`usFdaType` = `drugApproval`) |
| FDA Press Releases             | usFda (`usFdaType` = `pressAnnouncement`) |
