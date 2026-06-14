# Justification and Explanation

## Final Choice

The selected showcase pipeline is:

```text
count_basic__logreg_balanced
```

This combines a simple CountVectorizer with balanced Logistic Regression.

## Why These 4 Vectorizers Were Selected

| Vectorizer | Reason |
| --- | --- |
| `count_basic` | Simple word-frequency baseline; easy to explain and very fast |
| `tfidf_word_1_2` | Strong classic text baseline that captures words and short phrases |
| `tfidf_char_3_5` | Useful for Hinglish, spelling variation, abbreviations, and hashtags |
| `hashing_word` | Efficient and scalable because it does not store a vocabulary |

These four cover different vectorizer families instead of submitting near-duplicates.

## Why These 4 Classifiers Were Selected

| Classifier | Reason |
| --- | --- |
| `multinomial_nb` | Very fast and strong baseline for text classification |
| `logreg_balanced` | Reliable linear baseline with balanced class handling |
| `linear_svc` | Strong sparse-text classifier with good generalization |
| `sgd_log` | Fast linear model that can scale to larger datasets |

The selected classifiers are lightweight and explainable. No heavy models were used because the sprint rewards efficiency and suitability, not only raw accuracy.

## 80-Row Result Summary

The top pipeline on the 80-row experiment was:

```text
count_basic__logreg_balanced
```

| Metric | Value |
| --- | ---: |
| Accuracy | 0.650 |
| Macro-F1 | 0.651 |
| Weighted-F1 | 0.633 |
| Final score | 80.54 |
| Model size | 17 KB |

## Trade-Offs

Macro-F1 was not the only selection signal. The lab scoring formula also rewards speed, model size, and simplicity, which matters because the sprint asks for useful and efficient components instead of bulky models.

Balanced Logistic Regression with CountVectorizer is a good final choice because it is simple, fast, small, explainable, and produced the best final score on the 80-row experiment.
