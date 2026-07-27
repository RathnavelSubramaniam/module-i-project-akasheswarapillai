# Stock News Sentiment Analysis using AI

## What is this project?

This project uses AI to read stock market news and figure out if the news is **positive, negative, or neutral**. It then checks if this news sentiment matches how the stock price actually moved.

Think of it like this: if a company gets good news, does the stock usually go up? This project tries to teach a computer to answer that question automatically.

---

## What data is used?

A dataset of daily news articles about one company, along with that day's stock price and trading volume.

| Column | What it means |
|---|---|
| `Date` | Date of the news |
| `News` | The news article text |
| `Open` | Stock price at market open |
| `High` | Highest price that day |
| `Low` | Lowest price that day |
| `Close` | Stock price at market close |
| `Volume` | Number of shares traded |
| `Label` | Sentiment of the news: -1 = negative, 0 = neutral, 1 = positive |

**Size:** 349 rows, 8 columns. No missing or duplicate data.

---

## How the project works (step by step)

1. **Load and clean the data** — check for missing values, duplicates, and fix data types.
2. **Explore the data** — make charts to understand sentiment patterns, price trends, and news length.
3. **Convert news text into numbers** — computers can't read text directly, so we turn each news article into a list of numbers (called an "embedding"). Three methods were tried:
   - Word2Vec
   - Sentence Transformer (BAAI/bge-base-en-v1.5)
   - Sentence Transformer (all-MiniLM-L6-v2)
4. **Train models to predict sentiment** — using two types of models on each embedding:
   - Random Forest
   - Neural Network
5. **Compare all models** — check which combination predicts sentiment best on new, unseen news.

---

## Which model worked best?

**all-MiniLM-L6-v2 embeddings + Neural Network** was the winner.

- Test accuracy: **58.6%**
- Test F1-score: **0.577** (highest of all models tried)

### Why this one?
- It performed best on data it had never seen before.
- Random Forest models memorized the training data instead of learning general patterns (a problem called **overfitting**) — they scored 100% on training data but dropped to 40-50% on new data.
- The Neural Network with MiniLM embeddings avoided this problem and generalized better.

---

## Main takeaways

- Simple embeddings (Word2Vec) did not capture news meaning as well as sentence transformers.
- Neural Networks generalize better than Random Forest for this task.
- MiniLM + Neural Network is the best combination found so far.

## What could be improved next

- Fix Random Forest's overfitting using tuning and cross-validation.
- Try more advanced models or add more training data.
- Combine news sentiment with stock price trends for even better predictions.

---

## How to run this project

1. Download or clone this repository.
2. Open `Project_I_GenAI.ipynb` in Jupyter Notebook or Google Colab.
3. Install the required libraries:
   ```bash
   pip install numpy==1.26.4 scikit-learn==1.6.1 scipy==1.13.1 gensim==4.3.3 sentence-transformers==3.4.1 pandas==2.2.2
   ```
4. Make sure the dataset file `stock_news.csv` is in the same folder (or update the file path in the notebook).
5. Run the notebook from top to bottom.

---

## Files in this repository

```
├── Project_I_GenAI.ipynb   # The main notebook with all the code
├── stock_news.csv          # The dataset used
└── README.md                # This file
```

---

## Tools and libraries used

- **Python** — programming language
- **pandas, numpy** — for handling data
- **matplotlib, seaborn** — for making charts
- **gensim** — for Word2Vec embeddings
- **sentence-transformers** — for sentence embeddings
- **scikit-learn** — for Random Forest models
- **PyTorch** — for Neural Network models
