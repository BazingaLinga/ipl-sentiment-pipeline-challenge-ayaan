# ipl-sentiment-pipeline-challenge-ayaan
# IPL Text Sentiment Analyzer

This project trains and compares 16 lightweight machine-learning pipelines for IPL fan-post sentiment analysis. It is designed for the `ipl_sentiment_small_dataset.csv` dataset, an 80-row IPL sentiment dataset with positive, neutral, and negative Indian-English posts.

## Dataset

Default dataset:

```text
dataset/ipl_sentiment_small_dataset.csv
```

Expected columns:

| Column | Meaning |
| --- | --- |
| `statement` | IPL post text |
| `subject_keyword` | Team or subject keyword, such as MI, RCB, CSK, DC, KKR |
| `sentiment` | Target label: `positive`, `neutral`, or `negative` |

The trainer also supports similar CSVs that use `tweet`, `Post text`, `Post Keyword`, and `Sentiment`.

## Pipelines

The experiment compares 4 vectorizers with 4 classifiers, giving 16 total pipelines.

### Vectorizers

| Vectorizer | Why it is useful |
| --- | --- |
| CountVectorizer Basic | Simple frequency baseline |
| TF-IDF word 1-2 grams | Strong text-classification default that captures short phrases |
| TF-IDF character 3-5 grams | Helpful for Hinglish spelling variations, hashtags, and informal typing |
| HashingVectorizer word | Lightweight memory-friendly option without storing a vocabulary |

### Classifiers

| Classifier | Why it is useful |
| --- | --- |
| Linear SVC | Strong lightweight classifier for sparse text features |
| Logistic Regression | Reliable baseline with interpretable linear behavior |
| SGD log-loss | Fast linear model, good for scaling later |
| Complement Naive Bayes | Lightweight Naive Bayes variant that works well on text |

## Setup

```powershell
py -m pip install -r requirements.txt
```

## Train and Select the Best Pipeline

```powershell
py src/train_pipelines.py
```

The script will:

1. Load the 80-row IPL sentiment dataset.
2. Combine the team keyword with the post text as `subject_keyword [SEP] statement`.
3. Train and evaluate all 16 pipelines.
4. Compare accuracy, macro-F1, speed, model size, and simplicity.
5. Save the best showcase model and a JSON submission.

Outputs are saved in:

```text
artifacts/
```

Important files:

| File | Purpose |
| --- | --- |
| `results_80R.csv` | Ranked comparison of all 16 pipelines from the 80-row experiment |
| `submission_manifest.json` | Final 4 vectorizer + 4 classifier recipe submission |
| `completed_notebook.ipynb` | Completed notebook version of the experiment |
| `best_ipl_sentiment_pipeline.pkl` | Best trained pipeline |
| `model_card.md` | Model summary, metrics, intended use, and limitations |
| `JUSTIFICATION.md` | Explanation of final choices and trade-offs |

The `artifacts/` folder also keeps generated copies such as `pipeline_results.csv`, `pipeline_results.json`, and `best_model_report.txt`.

## GitHub Submission Checklist

The repository includes:

| Expected file | Status |
| --- | --- |
| `README.md` | Included |
| `completed_notebook.ipynb` | Included |
| `submission_manifest.json` | Included |
| `results_80R.csv` | Included |
| `results_300R.csv` | Not included because the final run uses the 80-row round |
| `.pkl` model file | Included as `best_ipl_sentiment_pipeline.pkl` |
| `model_card.md` | Included |
| Justification/explanation file | Included as `JUSTIFICATION.md` |
| `requirements.txt` | Included |

## Predict Sentiment

After training:

```powershell
py src/predict_sentiment.py "bhai RCB finally played like champions today" --team RCB
```

Example output:

```text
sentiment: positive
```

## Showcase Recommendation

For a project showcase, use the top-ranked pipeline from `artifacts/pipeline_results.csv`. Prefer macro-F1 over plain accuracy because the task has three sentiment classes and macro-F1 treats each class equally.

Current best pipeline from the 80-row run:

```text
count_basic__complement_nb
```

Top candidates from the latest run:

1. CountVectorizer Basic with Complement Naive Bayes
2. HashingVectorizer word with Complement Naive Bayes
3. TF-IDF character 3-5 grams with Complement Naive Bayes

Character n-grams are especially useful for Hinglish because users write the same Hindi/English words in many informal spellings.

