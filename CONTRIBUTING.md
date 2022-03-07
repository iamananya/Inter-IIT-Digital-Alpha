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

5. After geeting the json files delete the `FILLINGS_METADATA.csv` and `RAW_FILLINGS` to prevent overlap of files.

6. Proceed to step 1 again 


# Note 
- Edit the CIK.csv file with the tickers which we need to extract . Running all the tickers together will keep you waiting for hours XD