# ChronoMiner - NQ Futures Data Contract Splitter

ChronoMiner is a Python notebook utility for parsing, splitting, and organizing raw NQ (Nasdaq futures) intraday data into contract-specific and yearly CSV files. It is designed to help traders and analysts efficiently manage large datasets for backtesting and research.

## Features
- **Contract Calendar Generation:**
  - Automatically builds a list of NQ contracts (H, M, U, Z) for each year in a specified range, with correct start and end times based on the third Friday expiration rule.
- **Raw Data Parsing:**
  - Reads all raw CSV files from a folder, extracts contract codes from filenames, and assigns each row to the correct contract window.
- **Timezone Handling:**
  - Converts all timestamps to 'America/New_York' timezone for consistency.
- **Post-Parse Output:**
  - Saves each contract's data as a separate CSV file, named by its date range, in a 'Post Parse' folder.
- **Yearly Aggregation:**
  - Combines all post-parse files, sorts by time, and splits the master dataset into yearly CSVs for easy access.

## How It Works
1. **Contract Calendar:**
   - The notebook defines a function to generate contract start/end times for each year, following CME rules (third Friday expiration, roll 1 week prior, new contract starts Sunday 18:00).
2. **Raw File Processing:**
   - For each raw CSV, the contract code is extracted from the filename.
   - Data is filtered to only include rows within the contract's active window.
   - Each filtered contract file is saved with its date range.
3. **Yearly File Creation:**
   - All post-parse files are concatenated and sorted.
   - Data is split by year and saved as separate yearly CSVs.

## Requirements
- Python 3.8+
- pandas
- glob
- os
- re

Install requirements with:
```bash
pip install pandas
```

## Usage
1. Place your raw NQ CSV files in the `D:\Youtube\Data\Raw Data` directory.
2. Run the notebook `chronominer.ipynb`.
3. Post-parse contract files will be saved in `D:\Youtube\Data\Post Parse`.
4. Yearly files will be saved in `D:\Youtube\Data\Yearly Data`.

## Output Example
- `Post Parse/2022-03-13 to 2022-06-17.csv` (contract window)
- `Yearly Data/2022_NQ.csv` (all NQ data for 2022)

## Customization
You can adapt ChronoMiner to work with other futures symbols, such as YM (Dow Jones) or ES (S&P 500), by:
- Changing the contract code pattern in the regular expression (e.g., replace `NQ` with `YM` or `ES` in the code and filename matching logic).
- Adjusting any symbol-specific folder or file naming conventions as needed.
- Ensuring your raw data files use the correct symbol in their filenames (e.g., `YMZ2025.csv`).

This allows you to use the same workflow for different futures markets with minimal changes.

---

**Author:** livefreeordie_t (https://x.com/livefreeordie_t)
**Last updated:** July 2025
