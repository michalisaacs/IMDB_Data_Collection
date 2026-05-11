# Movie Dataset Enrichment & Financial Normalization

## Project Overview
This project focuses on the construction and enrichment of a high-quality movie dataset by integrating structured data from **IMDb** with unstructured information scraped from **Wikipedia**. The primary goal was to develop a robust data engineering pipeline that collects, cleans, and normalizes financial data and plot summaries to provide a reliable foundation for future predictive modeling.

## Technical Architecture & Implementation

### 1. Data Acquisition & Filtering
The pipeline begins by processing IMDb's public TSV datasets. We implemented a strict filtering logic to include only entries classified as `movie`, effectively excluding TV shows, shorts, and documentaries to maintain a focused dataset for analysis.

### 2. Advanced Web Scraping Engine
To overcome the inconsistencies in Wikipedia's entry naming, we developed a sophisticated scraping mechanism:
* **Candidate URL Algorithm:** A priority-based function that generates multiple URL variations (combining titles, release years, and the `(film)` suffix) to ensure the highest possible match rate.
* **Content Validation:** A critical validation layer ensures that the scraped page contains a cinematic `infobox`, preventing the collection of irrelevant data from disambiguation or non-movie pages.
* **Plot Extraction:** An intelligent parser that identifies various section headers (`Plot`, `Synopsis`, `Summary`) and extracts the descriptive text while maintaining narrative continuity.

### 3. Financial Normalization Logic
A core feature of this project is the conversion of diverse financial data into a standardized format:
* **Currency Conversion:** Automated detection and conversion of dozens of global currencies (USD, EUR, GBP, INR, etc.) based on defined exchange rates.
* **Regional Unit Handling:** specialized logic to process Indian numbering units like `Crore` (10M) and `Lakh` (0.1M).
* **Data Cleaning:** Utilization of Regular Expressions (Regex) to strip footnotes, handle range values (averaging budgets like "8-10 million"), and filter out non-monetary metrics like ticket admissions.
* **Standardization:** All financial outputs are converted to a unified numerical scale: **Millions of USD (M$)**.

## Missing Values Analysis (Final Run)
Following the final execution on the 5,000-movie sample, the dataset shows high integrity in foundational fields while reflecting the inherent challenges of scraping unstructured financial data. Foundational attributes such as movie identifiers and titles maintain complete documentation with zero missing values. The Plot extraction engine achieved a notable success rate, with only 37.66% missing values, indicating successful retrieval for the majority of the dataset. Financial metrics remain the most challenging to capture from open-source text, resulting in 74.52% missing values for Budget and 81.34% for Box Office revenue. Core metadata such as country and language show reliable coverage with approximately 20% missing values, demonstrating the effectiveness of the scraper in identifying the correct Wikipedia entries for the vast majority of the processed titles.

## System Dependencies
The execution of the notebook requires the following Python libraries:
* `pandas` & `numpy` for data manipulation.
* `requests` & `beautifulsoup4` for web scraping.
* `re` for complex string cleaning and Regex.
* `python-dotenv` for environment variable management.

---
**Developed as part of Assignment #1 in the Advanced Data Mining course, 2026.**
