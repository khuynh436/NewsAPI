# Financial News Sentiment Analysis

A Python project that scrapes financial news headlines, runs sentiment analysis, and correlates the results against S&P 500 market data. Built to accompany a Medium article series on data science and NLP.

---

## What it does

- Pulls financial news headlines from NewsAPI across configurable search queries
- Cleans and normalizes financial language using a custom term map
- Scores sentiment using VADER (Valence Aware Dictionary and sEntiment Reasoner)
- Fetches S&P 500 daily price data via yfinance
- Produces four charts:
  - Sentiment distribution across all headlines
  - Daily sentiment overlaid against S&P 500 price
  - Lag correlation between sentiment and next-day market returns
  - Average sentiment broken down by news source
- Exports results to CSV for further analysis

---

## Project structure

```
news-sentiment/
├── news_sentiment.py        # main script
├── requirements.txt         # dependencies
├── README.md
└── outputs/
    ├── fig1_sentiment_distribution.png
    ├── fig2_sentiment_vs_market.png
    ├── fig3_lag_correlation.png
    ├── fig4_sentiment_by_source.png
    ├── news_sentiment_results.csv
    └── news_sentiment_market_merged.csv
```

---

## Quickstart

### 1. Prerequisites

Make sure Python 3.8 or higher is installed. Download it from [python.org](https://python.org/downloads) — check **"Add Python to PATH"** during installation.

Verify your install:
```bash
python --version
```

### 2. Clone the repo

```bash
git clone https://github.com/yourusername/news-sentiment.git
cd news-sentiment
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Get a NewsAPI key

Sign up for a free key at [newsapi.org](https://newsapi.org). The free tier gives you:
- 100 requests per day
- Up to 30 days of historical headlines

Paste your key into `news_sentiment.py`:
```python
NEWS_API_KEY = "YOUR_KEY_HERE"
```

### 5. Run the script

```bash
python news_sentiment.py
```

Charts will be saved to the current directory. Results will be exported to `news_sentiment_results.csv` and `news_sentiment_market_merged.csv`.

---

## Configuration

At the top of `news_sentiment.py` you can adjust:

| Variable | Default | Description |
|---|---|---|
| `QUERIES` | 5 financial terms | Search queries sent to NewsAPI |
| `MARKET_TICKER` | `^GSPC` | Yahoo Finance ticker (S&P 500) |
| `DAYS_BACK` | `30` | How many days of headlines to pull |
| `POST_LIMIT` | `100` | Max articles per query |

---

## Want more historical data?

The free NewsAPI tier caps out at 30 days. For longer windows, use the **GDELT Project** — it's completely free, requires no API key, and covers up to a full year of global news.

A drop-in `fetch_gdelt()` function is included at the bottom of `news_sentiment.py`. Just uncomment it and swap it in for `fetch_headlines()`.

---

## Dependencies

```
requests
pandas
matplotlib
seaborn
vaderSentiment
yfinance
```

Install all at once:
```bash
pip install -r requirements.txt
```

---

## Limitations

- VADER is a general-purpose sentiment model, not finance-specific. For better accuracy on financial text, consider swapping in [FinBERT](https://huggingface.co/ProsusAI/finbert) — a transformer model fine-tuned on financial language. A FinBERT version of this project is in progress.
- 30 days of data is enough to observe patterns but not enough to draw statistically robust conclusions. Extend to 6–12 months via GDELT for more reliable results.
- NewsAPI free tier does not include full article body text — only title and description. Sentiment is scored on those fields only.

---

## Next steps

- [ ] Swap VADER for FinBERT and compare outputs
- [ ] Extend to 12 months using GDELT
- [ ] Test sentiment as a signal specifically around Fed announcement dates
- [ ] Add a Streamlit dashboard for interactive exploration

---

## License

MIT — use it, adapt it, build on it.
