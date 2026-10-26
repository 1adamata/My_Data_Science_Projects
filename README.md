# My Data Science Projects

This repository contains my projects related to Data Science.

## Table of Contents
- [Projects](#projects)
  - [Video Game Market Dataset Preprocessing](#video-game-market-dataset-preprocessing)
  - [Moscow Food-Service Market EDA](#moscow-food-service-market-eda)
- [Getting Started](#getting-started)
- [Repository Structure](#repository-structure)
- [How to Navigate](#how-to-navigate)
- [Datasets](#datasets)
- [Notebooks](#notebooks)
- [Scripts](#scripts)
- [Reports](#reports)

## Projects

| Project | Notebook | Topic | Stack |
|---|---|---|---|
| Video Game Market Dataset Preprocessing | [`notebooks/videogames_market_preprocessing.ipynb`](notebooks/videogames_market_preprocessing.ipynb) | Data cleaning, preprocessing and categorization | pandas, numpy |
| Moscow Food-Service Market EDA | [`notebooks/moscow_food_service_market_eda.ipynb`](notebooks/moscow_food_service_market_eda.ipynb) | Exploratory data analysis, visualization and business recommendations | pandas, numpy, matplotlib, seaborn, phik |

### Video Game Market Dataset Preprocessing

Preparing a cleaned slice of historical video game data (2000–2013) for an article on
the development of the gaming industry in the early 21st century, with a focus on the
RPG genre.

**Data:** `datasets/new_games.csv` — 16,956 rows and 11 columns: title, platform, year
of release, genre, regional sales (NA / EU / JP / other), critic score, user score and
ESRB rating.

**What was done:**
- Converted the column names to `snake_case`.
- Converted `eu_sales`, `jp_sales` and `user_score` to numeric types, turning the string
  values `unknown` and `tbd` into missing values.
- Removed rows without a title, genre or release year, and converted `year_of_release`
  to an integer type.
- Filled missing regional sales with the average for the corresponding platform and
  release year; replaced a missing ESRB rating with the `UNKNOWN` indicator; left missing
  scores unfilled so as not to create artificial data.
- Normalized the text values by letter case, which removed implicit duplicates in the
  genre names, and dropped 235 explicit duplicates.
- Filtered the data to 2000–2013 and added the `user_score_category` and
  `critic_score_category` fields (high / medium / low score).

**Key results:**
- 512 rows removed during preprocessing (3.02% of the original data), leaving 16,444 rows.
- The final 2000–2013 slice (`df_actual`) contains 12,781 records.
- Top 7 platforms by number of games released: PS2 (2,127), DS (2,120), Wii (1,275),
  PSP (1,180), X360 (1,121), PS3 (1,087), GBA (811).

### Moscow Food-Service Market EDA

Exploratory analysis of the Moscow food-service market to help investors choose a format,
district and price level for a new venue.

**Data:** Yandex Maps and Yandex Business, summer 2022 (English versions of the datasets).
- `datasets/rest_info_en.csv` — 8,406 venues: name, address, district, category, opening
  hours, rating, chain flag and number of seats.
- `datasets/rest_price_en.csv` — 4,058 rows of price data: price category, average bill
  string, numeric average bill and cappuccino price. Linked to venues by `id`.

**What was done:**
- Merged the venue and price data with a left join on `id`; converted `seats` to `Int64`
  and `chain` to `int8`.
- Investigated missing values (mostly unfilled listings) and left them as they are, since
  imputing or dropping them would distort the data or lose more than half of it.
- Normalized names and addresses and removed 7 implicit duplicates (0.08%), leaving 8,399
  venues; added an `is_24_7` flag for round-the-clock venues.
- Explored categories, districts, chain share, seating (including outliers), ratings, the
  top 15 chains and the average bill by district; measured rating correlations with `phik`.

**Key results:**
- Cafes (28%), restaurants (24%) and coffee shops (17%) are the most common venues.
- The Central district holds 27% of all venues and, together with the Western district, has
  the highest median bill (1,000 ₽); the South-East is the cheapest (450 ₽).
- 62% of venues are non-chain, but bakeries, pizzerias and coffee shops are more than half
  chains. Shokoladnitsa (120 venues) is the largest chain.
- Ratings are high and similar across categories (4.05–4.39); rating is only weakly related
  to other features, most strongly to price category (phik 0.22).
- Recommendations: a restaurant or bar in the upper price segment, with the Western or
  North-West district as a less saturated alternative to the centre, and 60–90 seats.

## Getting Started

```bash
python -m venv .venv
.venv/Scripts/activate
pip install -r notebooks/requirements.txt
jupyter lab
```

The notebooks read the data with paths relative to the `notebooks/` directory
(for example `../datasets/new_games.csv`), so run them from that folder.

## Repository Structure

```text
.
├── projects/
├── datasets/
├── notebooks/
├── scripts/
└── reports/
```

## How to Navigate
- Use `projects/` for complete project folders.
- Keep raw or processed data in `datasets/`.
- Put exploratory and analysis notebooks in `notebooks/`.
- Store reusable Python/R scripts in `scripts/`.
- Save final findings, summaries, and outputs in `reports/`.

## Datasets
Store datasets used across projects in `datasets/`.

| File | Description |
|---|---|
| `new_games.csv` | Historical data on video game sales and scores, 16,956 rows |
| `rest_info_en.csv` | Moscow food-service venues from Yandex Maps (2022), 8,406 rows |
| `rest_price_en.csv` | Price data for Moscow food-service venues, 4,058 rows |

## Notebooks
Keep Jupyter notebooks and experiments in `notebooks/`. Shared dependencies are listed
in `notebooks/requirements.txt`.

| File | Description |
|---|---|
| `videogames_market_preprocessing.ipynb` | Preprocessing and categorization of the video game market data |
| `moscow_food_service_market_eda.ipynb` | Exploratory analysis of the Moscow food-service market with recommendations |

## Scripts
Keep reusable scripts and utilities in `scripts/`.

## Reports
Keep final reports and result summaries in `reports/`.

## License
Released under the [MIT License](LICENSE).
