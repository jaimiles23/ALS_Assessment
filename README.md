# ALS_DataEngineer_Assessment
ALS Hiring Data Engineer exercises manipulating and aggregating large datasets with pandas.

## Requirements
This repository uses [jupyter notebooks](https://github.com/jupyter/notebook) 

TODO:
- ref other repos for jupyter nb install instrucitons?

Install data analysis requirements with:

```
pip install -r requirements.txt
```

## Exercises

### Question 1
**Produce a “people” file with the following schema. Save it as a CSV with a header line to the working directory.**
    
| Column | Type | Description |
| :-- | :-- | :-- |
|email | string | Primary email address | 
|code | string | Source code |
|is_unsub | boolean | If primary email address is unsubscribed |
|created_dt | datetime | Person creation datetime |
| pdated_dt | datetime | Person updated datetime |


### Question 2
**Use the output of #1 to produce an “acquisition_facts” file with the following schema that aggregates stats about when people in the dataset were acquired. Save it to the working directory.**

| Column | Type | Description | 
| :-- | :-- | :-- |
| acquisition_date | date | Calendar date of acquisition | 
| acquisitions | int | Number of constituents acquired on acquisition date |


## Data Files

The following 3 data sources are used:
1. [Constituent Information](https://als-hiring.s3.amazonaws.com/fake_data/2020-07-01_17%3A11%3A00/cons.csv), saved as `cons.csv`
2. [Constituent Email Addresses](https://als-hiring.s3.amazonaws.com/fake_data/2020-07-01_17%3A11%3A00/cons_email.csv), saved as `cons_email.csv`
3. [Constituent Subscription Status](https://als-hiring.s3.amazonaws.com/fake_data/2020-07-01_17%3A11%3A00/cons_email_chapter_subscription.csv), saved as `cons_email_chapter_subscription.csv.`

*Note*: Boolean columns (including is_primary) in all of these datasets are 1/0 numeric values. 1 means True, 0 means False.


## TODO:
- Assumptions section
- Results section
