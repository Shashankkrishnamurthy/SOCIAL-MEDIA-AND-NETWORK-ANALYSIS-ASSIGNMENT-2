COSC2671 Social Media and Network Analysis
Assignment 2 — Postgraduate Group 44

Who Shapes the Narrative? Network Influence and Sentiment Dynamics in AI Discourse on YouTube

RMIT University | School of Computing Technologies | Master of Data Science

Team Members:
- Bhuvan Palanikumar (S4138517)
- Shashank Krishnamurthy (S4141768)
- Thrupthi Bhojraj (S4140790)

Project Overview:

This project analyses 81,672 YouTube comments about artificial intelligence to investigate whether sentiment in AI discourse is shaped more by individual channel influence or by audience community membership. The pipeline combines VADER sentiment scoring, keyword-based topic modelling, NRC emotion lexicon analysis, and a Jaccard-weighted channel co-engagement network analysed with Louvain community detection and PageRank.

File Structure

├── S4141786_PG44.ipynb          # Main analysis notebook (run this)
├── README.md                      # This file
├── data/
│   ├── sample_submission.csv      # Representative 5,000-comment sample (<10MB)
│   ├── raw_youtube_comments.csv   # Raw collected comments (not included, >10MB)
│   ├── processed_comments.csv     # Cleaned analytic corpus (not included, >10MB)
│   ├── centrality_scores.csv      # Per-channel centrality measures
│   ├── community_profiles.csv     # Community-level summary statistics
│   ├── channel_sentiment.csv      # Per-channel average sentiment
│   ├── community_sentiment.csv    # Per-community average sentiment
│   ├── topic_sentiment.csv        # Per-topic average sentiment
│   ├── broker_removal.csv         # Broker removal experiment results
│   └── videos_collected.csv       # Metadata for collected videos
└── figures/
    ├── fig0_data_overview.png
    ├── fig2_sentiment_distribution.png
    ├── fig3_network.png
    ├── fig3b_network_full.png
    ├── fig4_top_channels.png
    ├── fig5_topics.png
    ├── fig5b_topic_wordclouds.png
    ├── fig6_community_sentiment.png
    ├── fig7_pagerank_vs_sentiment.png
    ├── fig8_sentiment_over_time.png
    └── fig9_topic_sentiment.png

How to Run:

1. Install required packages

bash
pip install pandas numpy matplotlib seaborn networkx python-louvain
pip install vaderSentiment wordcloud nltk scikit-learn google-api-python-client

Or install all at once:

bash
pip install -r requirements.txt


2. API Key (for data collection only)

If re-running the data collection stage, add your YouTube Data API v3 key in **Stage 1** of the notebook where indicated:

python
API_KEY = "YOUR_API_KEY_HERE"

If you already have the data files, skip Stage 1 and load directly from `data/raw_youtube_comments.csv`.

3. Run the notebook

Open S4141768_PG44.ipynb in Jupyter Notebook or JupyterLab and run cells **in order from top to bottom**.

Key stages:
| Stage | Description |
|-------|-------------|
| Stage 0 | Data overview and exploratory plots |
| Stage 1 | Live YouTube API data collection (skip if data exists) |
| Stage 2 | Text preprocessing and cleaning |
| Stage 3A | VADER sentiment analysis |
| Stage 3B | Keyword topic modelling + word clouds |
| Stage 4 | Network construction and centrality |
| Stage 5 | Community detection (Louvain) |
| Stage 6 | Statistical validation and robustness experiments |
| Stage 7 | Visualisation and figure export |

All figures are saved automatically to the `figures/` folder.


Dependencies:

| Package | Purpose |
|---------|---------|
| `pandas`, `numpy` | Data manipulation |
| `matplotlib`, `seaborn` | Visualisation |
| `networkx` | Network construction and analysis |
| `python-louvain` (`community`) | Louvain community detection |
| `vaderSentiment` | Sentiment scoring |
| `wordcloud` | Topic word clouds |
| `nltk` | Text preprocessing |
| `scikit-learn` | Statistical utilities |
| `google-api-python-client` | YouTube Data API v3 |

Reproducibility:

The pipeline is deterministic given a fixed random seed (`seed=42`) for spring layout, Louvain initialisation, and Independent Cascade simulation. The configuration-model null is stochastic but stable at the reported mean and standard deviation across 30 rewirings. All intermediate outputs are saved as CSV files in `data/`.

Notes:

- Large files (`processed_comments.csv`, `raw_youtube_comments.csv`, `checkpoint_comments.pkl`) are excluded from the repository due to size. Use `sample_submission.csv` to verify data structure.
- Do not include API keys, access tokens, or credentials anywhere in the repository.
- Expected runtime for the full pipeline (excluding data collection): ~10–15 minutes on a standard laptop.
