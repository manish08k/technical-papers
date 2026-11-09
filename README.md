# Maharashtra Company Registration Analytics

Analyses Maharashtra company master data with Python and Matplotlib.

## Charts (saved in `plots/`)
1. `chart1_authorised_capital_histogram.png` - companies per authorised
   capital interval: `<= 1L`, `1L to 10L`, `10L to 1Cr`, `1Cr to 10Cr`,
   `> 10Cr` (1L = 100,000; 1Cr = 10,000,000). Log y-axis is used
   automatically if the counts differ by more than 100x.
2. `chart2_registrations_by_year.png` - registrations per year.
3. `chart3_registrations_by_district_2015.png` - top 15 districts by
   registrations in 2015 (via PIN code).
4. `chart4_top_activities_last_10_years.png` - grouped bars: top five
   principal business activities across the latest 10 registration years.

## Data sources
- Company data: https://data.gov.in/catalog/company-master-data
  (Maharashtra file, saved as `data/company_master_maharashtra.csv`).
- PIN-code mapping: https://www.goldenchennai.com/pin-code/maharashtra-postal-code/
  Run `python build_pincode_mapping.py` to build `data/pincode_district.csv`
  from the page (or save the page as HTML and use `--html-file page.html`).
  The script only copies rows that have a 6-digit PIN and a district. The
  mapping is NOT verified to be complete; the program reports how many PIN
  codes could not be matched.

## Requirements
Python 3.10+.

## Structure
```text
analysis.py              data loading, cleaning, aggregation
visualization.py         Matplotlib charts
main.py                  runs everything
build_pincode_mapping.py builds data/pincode_district.csv
test_analysis.py         unittest tests
data/  plots/
```

## Setup
```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements-dev.txt
```
`requirements.txt` holds runtime dependencies (matplotlib);
`requirements-dev.txt` adds flake8. After installing, verify with
`pip freeze`.

## Run
```bash
python build_pincode_mapping.py   # once, needs internet
python main.py                    # optional: --year 2015 --company-csv PATH
python -m unittest -v             # tests
flake8                            # lint (config in .flake8)
```

## Data-cleaning decisions
- Column names are matched case-insensitively against aliases in
  `analysis.py` (`COLUMN_ALIASES`); edit them if the real headers differ.
- Capital: commas removed; blank, non-numeric, NaN/inf and negative values
  are excluded from chart 1 and counted. Zero is valid (`<= 1L`).
  Intervals are upper-inclusive, so each value falls in exactly one.
- Dates: several formats are tried (day-first). Unparseable dates, years
  before 1850 and future dates are excluded from charts 2-4 and counted.
  Check the real format; two-digit years are ambiguous.
- PIN code: the 6-digit number at the very end of the address. Missing or
  unmatched PINs are counted, never given a made-up district.
- Missing business activity is excluded from chart 4 and counted.
- No row is deleted; all exclusions are printed by `main.py`.

## Known limitations
- Registered address PIN may not reflect the actual operating location.
- Company master data is a snapshot; struck-off companies may be absent.
- District names depend on the web page and may be outdated.

## Git / GitLab
```bash
git init
git add .
git commit -m "Maharashtra company analytics"
git branch -M main
git remote add origin https://gitlab.com/<your-username>/<repo-name>.git
git push -u origin main
```
