# stock-direction-predictor

Trying to predict whether a stock goes **up or down** the next day — not the exact price, just the direction. Turns out it's harder than it sounds.

Data comes from Yahoo Finance via `yfinance`. Features are basic stuff — moving averages, returns, RSI. Model is a Random Forest classifier. And everything gets compared against a coin-flip baseline, because that's the honest way to do it.

---

## what this actually does

- pulls historical OHLCV data (2015–2026) for US + Indian stocks
- builds features like 5/10/20-day moving averages, daily returns, RSI, volume ratio
- labels each day as `1` (stock went up next day) or `0` (went down)
- trains a Random Forest classifier
- backtests using walk-forward validation — no future data leakage
- compares results against a "just flip a coin" baseline

---

## stocks covered

| ticker | exchange |
|--------|----------|
| AAPL | NASDAQ |
| MSFT | NASDAQ |
| RELIANCE.NS | NSE |
| TCS.NS | NSE |
| HDFCBANK.NS | NSE |

---

## notebooks

| notebook | what it does |
|----------|-------------|
| `01_data_collection` | downloads and saves raw data |
| `02_feature_engineering` | builds all features and labels |
| `03_model_training` | trains + evaluates the classifier |
| `04_backtesting` | walk-forward backtest + comparison |

run them in order.

---

## setup

```bash
pip install -r requirements.txt
```

then open the notebooks in order.

---

## what i learned

markets are genuinely hard to predict. even with clean features and a decent model, you're often barely above 50%. the walk-forward backtest makes this very obvious — and that's kind of the point.

the reference LSTM project predicts prices and never checks if it actually beats anything. this project at least tries to be honest about what the model can and can't do.

---

## stack

Python 3.12 · yfinance · pandas · scikit-learn · matplotlib
