# Reddit Research Tool

A lightweight, read-only Python tool for collecting and analyzing publicly available Reddit post and comment data for personal research purposes. Built with [PRAW](https://praw.readthedocs.io/) (Python Reddit API Wrapper).

## Overview

This tool uses Reddit's official API to fetch public post metadata and comments from specified subreddits, storing them locally for offline trend analysis, sentiment analysis, and topic modeling. It is designed to be fully compliant with Reddit's [Data API Terms](https://redditinc.com/policies/data-api-terms) and [Responsible Builder Policy](https://support.reddithelp.com/hc/articles/42728983564564).

**This tool is strictly read-only.** It does not post, comment, vote, send messages, or perform any write operations on Reddit.

## Features

- **Read-only data collection** - Fetches post titles, scores, timestamps, comment counts, and comment text from public subreddits
- **Rate limit compliance** - Respects Reddit's API rate limits (stays well within 100 requests/minute) with built-in exponential backoff on 429 responses
- **Privacy-conscious** - Does not collect or store usernames or any personally identifiable information (PII)
- **Local storage only** - All data is stored in a local SQLite database; nothing is shared, published, or distributed
- **Configurable delays** - User-configurable request intervals to minimize API load

## Use Case

This tool is for personal, non-commercial research into how online discussions evolve across technology and science communities. Specific analyses include:

- **Trend analysis** - Tracking how discussion topics rise and fall over time within subreddits
- **Sentiment analysis** - Understanding community sentiment around specific topics using NLP
- **Topic modeling** - Identifying recurring themes and emerging topics across multiple communities

## Target Subreddits

- r/technology
- r/science
- r/dataisbeautiful
- r/programming
- r/machinelearning

Only publicly accessible subreddits are used. The tool does not access private or restricted communities.

## Tech Stack

- **Python 3.10+**
- **PRAW** - Reddit API wrapper for authenticated API access
- **SQLite** - Local database for data storage
- **spaCy / NLTK** - Natural language processing for sentiment and topic analysis
- **pandas** - Data manipulation and analysis
- **scikit-learn** - Topic modeling (LDA) and clustering

## Installation

```bash
git clone https://github.com/Natedog8/reddit-research-tool.git
cd reddit-research-tool
pip install -r requirements.txt
```

## Configuration

Copy the example config and add your Reddit API credentials:

```bash
cp config.example.ini config.ini
```

Edit `config.ini` with your Reddit app credentials:

```ini
[reddit]
client_id = YOUR_CLIENT_ID
client_secret = YOUR_CLIENT_SECRET
user_agent = reddit-research-tool/1.0 by u/natebarrett8
```

## Usage

```bash
# Collect recent posts from target subreddits
python collect.py --subreddits technology science programming --limit 100 --period month

# Run sentiment analysis on collected data
python analyze.py --type sentiment

# Generate topic model
python analyze.py --type topics --num-topics 10
```

## API Compliance

This tool is built with Reddit's policies at the forefront:

- **Read-only access** - No write operations of any kind
- **Rate limiting** - Built-in delays and exponential backoff; stays well within API limits
- **No PII collection** - Usernames and user data are excluded from all datasets
- **No commercial use** - Data is used solely for personal research and is never sold, licensed, or shared
- **No AI training** - Collected data is not used to train machine learning models for commercial purposes
- **Data retention** - Data is stored only as long as needed for active research and is deleted afterward

## License

MIT License - see [LICENSE](LICENSE) for details.

## Disclaimer

This tool is for personal, non-commercial research only. All usage must comply with Reddit's [Terms of Service](https://redditinc.com/policies/user-agreement), [Data API Terms](https://redditinc.com/policies/data-api-terms), and [Responsible Builder Policy](https://support.reddithelp.com/hc/articles/42728983564564). The author is not responsible for misuse of this tool.
