# Movie Genre Classification & Attribute Analysis

Exploratory data analysis (EDA) and a baseline genre classifier for a dataset of 50,000 feature films, plus an executive-style report.

> **Data caveat:** the dataset appears to be **synthetically generated**. Every category (genre, language, country, director, studio, and so on) is almost perfectly evenly distributed, and `Genre` is independent of every other column. As a result, the classifier performs no better than chance (about 14 %, i.e. 1 in 7). The project demonstrates the EDA and modelling workflow, not real-world industry findings.

## Repository structure

```
movie-genre-classification/
├── data/
│   └── movie_genre_classification_final_2.csv   # 50,000 films x 17 columns
├── notebooks/
│   └── 01_eda_and_genre_classification.ipynb    # EDA + baseline vs Random Forest
├── reports/
│   ├── Exhaustive_Movie_Analysis_Report.docx    # Executive report
│   └── figures/                                 # Distribution charts used in the report
├── requirements.txt
└── README.md
```

## Dataset columns

`Title`, `Year`, `Director`, `Duration`, `Rating`, `Votes`, `Description`, `Language`, `Country`, `Budget_USD`, `BoxOffice_USD`, `Genre`, `Production_Company`, `Content_Rating`, `Lead_Actor`, `Num_Awards`, `Critic_Reviews`

## Quick start

```bash
git clone https://github.com/dhappo/movie-genre-classification.git
cd movie-genre-classification

python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt

jupyter lab notebooks/01_eda_and_genre_classification.ipynb
```

The notebook uses relative paths, so launch it from the repository root or open it from the `notebooks/` folder. Set `SAVE_FIGURES = True` in the first code cell to regenerate the PNGs in `reports/figures/`.

## What the notebook covers

1. Data loading and inspection
2. Distributions of the seven categorical attributes
3. Interactive Plotly explorers (they only render when run locally, not on GitHub)
4. Release-year trends, overall and by country
5. Genre classification: majority-class baseline vs a Random Forest pipeline

## Key findings

| Model | Test accuracy |
|---|---|
| Chance (1 / 7 genres) | 14.3 % |
| Majority-class baseline | 14.4 % |
| Random Forest (one-hot + scaled numerics) | 14.4 % |

No feature in this dataset carries information about genre. An earlier version of the data contained a `Description` column that mapped one-to-one to `Genre`, which produced a misleading 100 % accuracy (target leakage). It is excluded here.

## Reproducibility

- `random_state=42` throughout
- Stratified 80/20 train/test split
- Tested with Python 3.12 / pandas 3.0 / scikit-learn 1.8
