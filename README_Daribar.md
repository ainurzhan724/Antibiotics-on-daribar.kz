# Pharmaceutical Price Analysis in Kazakhstan

**Python · Pandas · BeautifulSoup · SciPy · Matplotlib · Seaborn · Plotly**

## Project overview

This educational data analytics project explores the assortment and listed prices of antibacterial medicines on **Daribar.kz**, comparing **Astana** and **Almaty**. It also evaluates a hypothetical procurement scenario for a small pharmacy in **Petropavl**, where a lower purchase price may or may not offset higher transportation costs.

The project covers web scraping, data cleaning, exploratory data analysis (EDA), matched-product price comparisons, statistical testing, and a break-even calculation.

## Business questions

1. Which countries and manufacturers appear most frequently in the observed assortment?
2. How are listed medicine prices distributed?
3. Are comparable products priced differently in Astana and Almaty?
4. Under a simplified transportation-cost model, when would sourcing from Almaty become worthwhile for a pharmacy in Petropavl?

## Data

- **Source:** Public product listings on Daribar.kz.
- **Cities:** Astana and Almaty.
- **Initial volume:** Approximately 2,194 rows documented in the project presentation, before subsequent cleaning.
- **Main fields:** medicine name, city, dosage, dosage form, units per package, price, active ingredient, manufacturer, country of manufacture.
- **Data-quality limitation:** Some entries have missing prices and other product attributes; the presentation reports 1,041 non-null prices in an early dataset overview. Comparisons therefore use the available matched, priced records rather than every listing.

> The files represent a snapshot of listings, **not** current market prices or actual sales transactions.

## Approach

### 1. Data collection

Used `requests` and `BeautifulSoup` to extract product information from Daribar.kz listings, then exported it to CSV for analysis.

### 2. Data cleaning

- Standardized city and country names.
- Extracted dosage and package details from product names using regular expressions.
- Normalized active-ingredient descriptions, including alternative spellings and salt forms.
- Reviewed duplicate records and missing values.

### 3. Exploratory analysis

Explored the assortment by country, manufacturer, and dosage form, as well as price distributions and outliers. Visualizations were created with Matplotlib, Seaborn, and Plotly.

### 4. City-level price comparison

Matched product records across Astana and Almaty using a product identifier and calculated mean, median, absolute, and percentage price differences. Applied a paired **Wilcoxon signed-rank test** to the available matched prices.

The reliability of this comparison depends on correctly matching identical products, including their dose, dosage form, package size, and manufacturer.

### 5. Petropavl procurement scenario

Assumptions from the presentation:

| Variable | Almaty | Astana |
| --- | ---: | ---: |
| Distance to Petropavl | 1,718 km | 495 km |
| Assumed transport tariff | 250 KZT/km | 250 KZT/km |
| Modeled delivery cost | 429,500 KZT | 123,750 KZT |

**Additional delivery cost for sourcing from Almaty: 305,750 KZT.**

For a product that is cheaper in Almaty, the illustrative break-even quantity is:

```text
minimum_packages = ceil(305750 / (price_astana - price_almaty))
```

This is a simplified **single-product, full-shipment-cost** scenario. Actual procurement requires shipment consolidation, order volumes, availability, cold-chain requirements, storage conditions, and other logistics constraints.

## Findings

The presentation reports the following findings for the analyzed snapshot:

- **India** leads the observed assortment by represented products and unique manufacturers.
- **Almaty** has lower average observed prices than Astana for the compared products; the presentation reports a statistically significant matched-price difference, although the exact p-value is not documented there.
- **More than 90%** of the observed products fall within a price band of up to **5,000 KZT**.
- Some products appear cheaper to source from Almaty even after applying the simplified delivery model, but this does **not** establish profitability for real-world orders.
- Products manufactured in **Belarus, Russia, and India** tend to be cheaper within this dataset, while higher observed prices appear for several European countries. This is a descriptive comparison, not a causal conclusion.

## Repository contents

- `projectdaribar.py` — analysis script exported from Google Colab.
- `daribar_almaty.csv`, `daribar_astana.csv` — city-level data snapshots.
- `daribar_final (1).csv` — processed dataset snapshot.
- `Daribar презентация.pptx` — slides with analysis and visualizations.

## Reproducibility note

**The original script currently requires cleanup before it can be run end-to-end.** It references additional intermediate CSV files not present in the repository, and some lines need syntax/Pandas corrections. The available presentation and data files document the exploratory project, but the repository should not yet be described as a fully reproducible pipeline.

Recommended next steps:

1. Fix syntax and DataFrame operations in the script.
2. Consolidate cleaning steps and create or regenerate required intermediate datasets.
3. Validate the product-matching key and re-run the statistical test.
4. Export 3–5 representative charts as images and embed them here.
5. Add `requirements.txt` and, optionally, a cleaned Jupyter notebook.

## Scope and limitations

This is an **educational portfolio project**, not an operational pharmacy procurement system. Prices, stock availability, scraping behavior, and logistics tariffs may change. Results should not be interpreted as purchasing or medical advice.
