# Model Card: IPL Text Sentiment Analyzer

## Model Details

- **Task:** classify IPL text sentiment as `positive`, `neutral`, or `negative`
- **Selected pipeline:** `count_basic__logreg_balanced`
- **Vectorizer:** `CountVectorizer(max_features=3000, lowercase=True)`
- **Classifier:** `LogisticRegression(max_iter=1000, class_weight="balanced")`
- **Dataset:** `ipl_sentiment_small_dataset.csv`
- **Dataset size:** 80 rows
- **Model file:** `best_ipl_sentiment_pipeline.pkl`

## Intended Use

This model is intended for a student sprint/showcase project where the goal is to compare lightweight vectorizer and classifier combinations for IPL sentiment analysis. It is suitable for short IPL fan posts, Indian-English text, and simple Hinglish-style comments.

## Evaluation Summary

Latest 80-row experiment:

| Metric | Value |
| --- | ---: |
| Accuracy | 0.650 |
| Macro-F1 | 0.651 |
| Weighted-F1 | 0.633 |
| Final score | 80.54 |
| Approx. model size | 17 KB |

The model was selected because it had the best lab `final_score`, which rewards performance, speed, model size, and simplicity.

## Limitations

- The dataset is small, so scores may move noticeably with a different split.
- The model can miss sarcasm, jokes, and cricket context that requires deeper reasoning.
- It should not be treated as a production sentiment system without more data and validation.

## Ethical Notes

The model predicts sentiment from public-style IPL text only. It should not be used to profile individuals or make important decisions about people.
