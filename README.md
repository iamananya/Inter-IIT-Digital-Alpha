# EDGAR-CRAWLER
Crawl and fetch all publicly-traded companies annual reports from [SEC's EDGAR](https://www.sec.gov/edgar.shtml) database.

`edgar-crawler` is an optimized toolkit that retrieves textual information from financial reports, such as 10-K, 10-Q or 8-K filings.

More specifically, it can:
- Crawl and download financial reports for each publicly-traded company, for specified years, through the `edgar_crawler.py` module.
- Extract and clean specific text sections, such as Risk Factors, MD&A, and others, through the `extract_items.py` module. **Currently, we only support extraction of 10-K filings (i.e., annual reports).**

The purpose of EDGAR-CRAWLER is to speed up research and experiments that rely on financial information, as they are widely seen in the research literature of economics, finance, business and management.

## Table of Contents
- [Install](#install)
- [Usage](#usage)
- [Citation](#citation)
- [Accompanying Resources](#accompanying-resources)
- [Contributing](#contributing)
- [License](#license)

## Steps to extract forms from the tickers

# Info 
- CIK Numbers are avaiable in CIK.csv
- edgar_crawler.py to generate all the filings for the given cik numbers and duration
- extract_items_8k.py to extract all the 8k forms 
- extract_items_10k.py to extract all the 10k forms 
- extract_items_10q.py to extract all the 10q forms 
- INDICES contains files for the specified year (Hence on running the script those files are skipped. Don't get mad XD)

# Procedure

1. Edit the `config.json` file with `"filing_types": []` specify the form type as `8-K or 10-K or 10-Q` depending on the type of form we wish to extract

2. Run `edgar_crawler.py` . This will create a csv named `FILLINGS_METADATA.csv` alongwith a folder named `RAW_FILLINGS`

3. Run the corresponding script file in   `extract_items_{type mentioned in the config.json file}.py`

4. Creates a folder in the datasets directory corresponding to the form type 







## Usage
- Before running any script, you can edit the `config.json` file.
  - Arguments for `edgar_crawler.py`, the module to download financial reports:
      - `--start_year XXXX`: the year range to start from
      - `--end_year YYYY`: the year range to end to
      - `--quarters`: the quarters that you want to download filings from (List).<br> Default value is: `[1, 2, 3, 4]`.
      - `--filing_types`: list of filing types to download.<br> Default value is: `['10-K', '10-K405', '10-KT']`.
      - `--cik_tickers`: list or path of file containing CIKs or Tickers. e.g. `[789019, "1018724", "AAPL", "TWTR"]` <br>
        In case of file, provide each CIK or Ticker in a different line.  <br>
      If this argument is not provided, then the toolkit will download annual reports for all the U.S. publicly traded companies.
      - `--user_agent`: the User-agent that will be declared to SEC EDGAR.
      - `--raw_filings_folder`: the name of the folder where downloaded filings will be stored.<br> Default value is `'RAW_FILINGS'`.
      - `--indices_folder`: the name of the folder where EDGAR TSV files will be stored. These are used to locate the annual reports. Default value is `'INDICES'`.
      - `--filings_metadata_file`: CSV filename to save metadata from the reports.
      - `--skip_present_indices`: Whether to skip already downloaded EDGAR indices or download them nonetheless.<br> Default value is `True`.
  - Arguments for `extract_items.py`, the module to clean and extract textual data from already-downloaded 10-K reports:
    - `--raw_filings_folder`: the name of the folder where the downloaded documents are stored.<br> Default value s `'RAW_FILINGS'`.
    - `--extracted_filings_folder`: the name of the folder where extracted documents will be stored.<br> Default value is `'EXTRACTED_FILINGS'`.<br> For each downloaded report, a corresponding JSON file will be created containing the item sections as key-pair values.
    - `--filings_metadata_file`: CSV filename to load reports metadata (Provide the same csv file as in `edgar_crawler.py`)
    - `--items_to_extract`: a list with the certain item sections to extract. <br>
      e.g. `['7','8']` to extract 'Management’s Discussion and Analysis' and 'Financial Statements' section items.<br>
      The default list contains all item sections.
    - `remove_tables`: Whether to remove tables containing mostly numerical (financial) data. This work is mostly to facilitate NLP research and often numerical tables are not useful

- To download financial reports from EDGAR, run `python edgar_crawler.py`
- To clean and extract specific item sections from already-downloaded 10-K documents, run `python extract_items.py`.
  - Reminder: We currently support the extraction of 10-K documents. 


