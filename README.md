# Music Genre Dataset — COMP90049 Group Project (Group 41)

**Dataset**: [Prediction of Music Genre](https://www.kaggle.com/datasets/vicsuperman/prediction-of-music-genre) — Kaggle (~50,000 songs, 18 audio features)


## Research Questions
How machine learning can be used to improve music streaming services?

| Member | Notebook | Research Question |
|--------|----------|------------------|
| Pumi | `pumi/music_classifying_genres.ipynb` | Can audio features predict a song's genre? |
| Scott | `scott/music_modes_prediction.ipynb` | Can audio features predict musical mode (Major vs Minor)? |
| Udita | `udita/recommendation_of_music.ipynb` | Can a model recommend music based on genre, mode, and tempo? |
| Puze | `zed/popularity.ipynb` | Can audio features predict a song's popularity? |

---

## Prerequisites

Python 3.10+ with the following packages:

```bash
pip install pandas numpy scikit-learn matplotlib seaborn kagglehub
```

The dataset is downloaded automatically via `kagglehub` on first run and cached locally.

---

## How to Run

### Step 1 — Verify the shared data cleaning module

`data_cleaning.py` defines `load_and_clean()`, which every notebook imports.
No separate execution is needed — but you can verify it works in isolation:

```bash
cd music_ml
python3 -c "
from data_cleaning import load_and_clean
import kagglehub, os
path = kagglehub.dataset_download('vicsuperman/prediction-of-music-genre')
df = load_and_clean(os.path.join(path, 'music_genre.csv'))
print(df.shape)
"
```

Expected output:
```
Loaded:                        50,005 rows
After bad value removal:       40,560 rows
Exact duplicates removed:           0
Conflicting duplicates removed: 5,080
Final shape:                   (35480, 14)
```

---

### Step 2 — Visualise the cleaned dataset

Open and run `data_cleaning_visualisation.ipynb` to inspect the cleaned data before any research-specific processing:

```bash
jupyter notebook data_cleaning_visualisation.ipynb
```

Produces:
- Provenance bar chart (row count at each cleaning step)
- Genre and mode class distributions
- Numeric feature histograms
- Correlation heatmap

---

### Step 3 — Run each research question notebook

Each notebook is fully self-contained — it imports `load_and_clean()`, performs its own encoding and feature engineering, trains models, and evaluates results.
Run them in any order; they are independent of each other.

**Genre Classification — Pumi**
```bash
jupyter notebook pumi/music_classifying_genres.ipynb
```

**Mode Prediction (Major vs Minor) — Scott**
```bash
jupyter notebook scott/music_modes_prediction.ipynb
```

**Music Recommendation — Udita**
```bash
jupyter notebook udita/recommendation_of_music.ipynb
```

**Popularity Prediction — Zed**
```bash
jupyter notebook zed/popularity.ipynb
```

---

## Project Structure

```
music_ml/
├── README.md                          ← this file
├── data_cleaning.py                   ← shared cleaning module (imported by all notebooks)
├── data_cleaning_visualisation.ipynb  ← visualises the cleaned dataset
│
├── pumi/
│   └── music_classifying_genres.ipynb
├── scott/
│   └── music_modes_prediction.ipynb
├── udita/
│   └── recommendation_of_music.ipynb
└── zed/
    └── popularity.ipynb
```

---

## Shared Cleaning Pipeline (`data_cleaning.py`)

All notebooks call `load_and_clean(csv_path)` which applies the following steps identically:

1. **Bad value sweep** — removes rows containing `?`, `-1`, `'-1'`, empty strings, or `NaN` across all columns at once
2. **Tempo coercion** — converts `tempo` to float, drops any remaining non-numeric rows
3. **Exact duplicate removal** — drops fully identical rows
4. **Conflicting duplicate removal** — removes rows where the same `(artist_name, track_name)` pair has different categorical labels (e.g., same song assigned two different genres)
5. **Metadata columns dropped** — removes `artist_name`, `track_name`, `instance_id`, `obtained_date`

Feature engineering, encoding, and scaling are handled separately in each notebook.
