# ALS_DataEngineer_Assessment
ALS Hiring Data Engineer exercises manipulating and aggregating large datasets with pandas.


- [ALS_DataEngineer_Assessment](#als_dataengineer_assessment)
- [How to use](#how-to-use)
  - [Download](#download)
  - [Use etl_jupyternb.ipynb](#use-etl_jupyternbipynb)
  - [Use etl_script.py](#use-etl_scriptpy)
  - [Requirements](#requirements)
      - [Install Dependencies](#install-dependencies)
    - [Run script](#run-script)
- [Exercise Documentation](#exercise-documentation)
  - [Questions](#questions)
    - [Question 1](#question-1)
    - [Question 2](#question-2)
  - [Input data](#input-data)
    - [input data urls](#input-data-urls)
  - [Output data](#output-data)
    - [Output file data sources](#output-file-data-sources)
      - [People file data source](#people-file-data-source)
      - [Acquisition facts data source](#acquisition-facts-data-source)
  - [Keep relevant columns](#keep-relevant-columns)
  - [Relational joins](#relational-joins)
  - [Handling missing data](#handling-missing-data)
  - [Duplicate foreign keys](#duplicate-foreign-keys)
    - [df_emails.cons_id](#df_emailscons_id)
    - [df_subs.cons_email_ids](#df_subscons_email_ids)


# How to use
This section documents how to run the ETL script. Please note: input and output data files will automatically be downloaded and saved to the working directory.

This repository conducts analysis via 2 file types to show and/or perform data analysiss:
  1. **etl_jupyternb.ipynb**: a [jupyter notebooks](https://github.com/jupyter/notebook) that contains all documentation, additional exploratory data analysis, and produces the output files.. 
  2. **etl_script.py**: a python3 script that can be run via the terminal to produce the output files.


## Download 
This repository can be downloaded from GitHub via:

**Note: removed owner name for anonymity.
```
git clone https://github.com/{}/ALS_Assessment.git
```

## Use etl_jupyternb.ipynb
If you have Jupyter Notebooks installed, you can access the **etl_jupyternb.ipynb** locally. Otherwise, [NBViewer.org](http://nbviewer.org) renders a GitHub Jupyter Notebook online. 
<!-- You can access the notebook online [here](https://github.com/jaimiles23/ALS_Assessment/blob/master/etl_jupyternb.ipynb) -->


## Use etl_script.py
_Note:_ This section assumes you are using Windows OS.

## Requirements

Python verssion 3.6+

3rd party libraries documented in requirements.txt
- numpy
- matplotlib
- pandas 
- seaborn
- missingno
- pywrangle


#### Install Dependencies
To run this script, you must install the dependencies outlined in the requirements.txt file. I recommend using a virtual environment to manage these dependencies. Learn more [here](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

To run the .py script, navigate to the directory with the cloned repository and install the required dependencies using:
To install the dependencies with a virtual environment, navigate to the directory for the cloned repository and run 

```
python3 -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
deactivate
```

### Run script
After the dependencies have been installed, you can run the the etl_script.py from the command line using:

```
venv\Scripts\active
python etl_script.py
deactivate
```

NOTE:
- Activate the virtual environment to use the installed libraries
- Exclude the -m module command to run the script. 


# Exercise Documentation

## Questions
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


## Input data

### input data urls
The following 3 data sources are used:
1. [Constituent Information](https://als-hiring.s3.amazonaws.com/fake_data/2020-07-01_17%3A11%3A00/cons.csv), saved as `cons.csv`
2. [Constituent Email Addresses](https://als-hiring.s3.amazonaws.com/fake_data/2020-07-01_17%3A11%3A00/cons_email.csv), saved as `cons_email.csv`
3. [Constituent Subscription Status](https://als-hiring.s3.amazonaws.com/fake_data/2020-07-01_17%3A11%3A00/cons_email_chapter_subscription.csv), saved as `cons_email_chapter_subscription.csv.`

*Note*: Boolean columns (including is_primary) in all of these datasets are 1/0 numeric values. 1 means True, 0 means False.

## Output data
Both **etl_jupyternb.ipynb** and **etl_script.py** output two data files:
1. **people.csv**: contains solution data to question 1
2. **acquisition_facts.csv**: contains solution data to question 2


### Output file data sources
This section details the data sources for the different output files generated.

#### People file data source

This section details which dataframe is used to gather the data output in the persons file:

| Column | Type | Description | Dataframe source | 
| :-- | :-- | :-- | :-- |
|email | string | Primary email address | `df_emails.email` |
|code | string | Source code | `df_info.source` |
|is_unsub | boolean | If primary email address is unsubscribed | `df_subs.is_unsub` |
|created_dt | datetime | Person creation datetime | `df_info.create_dt` |
|updated_dt | datetime | Person updated datetime | `df_info.modified_dt` |


#### Acquisition facts data source
Data source for the acquisition data file

| Column | Type | Description | Data source |
| :-- | :-- | :-- | :-- |
| acquisition_date | date | Calendar date of acquisition | Date extracted from `created_dt` from people file | 
| acquisitions | int | Number of constituents acquired on acquisition date | Count() extracted from number of emails on `created_dt` |


## Keep relevant columns
To increase notebook performance and readability, I only keep columns that are relevant to the analysis.

Based on the questions outlined in this exercise and the columns identified in [Identify relevant information & entity relationships](#identify-relevant-information-&-entity-relationships), I am interested in the following columns for each dataframe:

**df_info:**
- `cons_id`: primary key, relates to other columns
- `source`: code string data for q1 table
- `create_dt`: created_dt datetime data for q1 table
- `modified_dt`: updated_dt datetime for q1 table

**df_emails:**
- `cons_email_id`: primary key
- `cons_id`: foreign key used to link to df_info
- `email`: email string data for q1 table

**df_subs:**
- `cons_email_chapter_subscription_id`: primary key
- `cons_email_id`: foreign key to link to df_emails
- `isunsub`: is_unsub boolean data for q1 table

## Relational joins
The three data files contain relational data with contain primary and foreign keys to connect information about users. Relational joins are required to retrieve the information for the people file.

I use `df_emails` as the base data file because it contains the most user records.
Left joins to the df_emails table are made to preserve email addresses. This is based on the assumption that email addresses are the variable of interest.

Given df_emails, the following left joins can be made:
- `df_emails.cons_email_id` = `df_subs.cons_email_id`
- `df_emails.cons_id` = `df_info.cons_id`

*NOTE*: Because I used a left_join, it's possible that there will be NULL values in merged columns.

## Handling missing data
The script handles missing data based on the intent of the data. 

Questions 1 and 2 are interested in the following data:
1. `email`
1. `code`
1. `is_unsub`
1. `created_dt`
1. `updated_dt`

`email` is the unique identifier for each row and used to count constituents 'acquired'. Additionally, I use the variable `create_dt` from the constituent information file to record acquisition dates. Because `email` is a primary key and `create_dt` is used to create the acquisition_facts.csv, I will drop records with NULL values in these fields.

The folloiwng data: `code`, `is_unsub`, and `updated_dt` are descriptive information about the constituent. This data is not necessary for the acquisition_facts output for question 2. As such, missing data in these columns will be filled witht he string "unknown".


## Duplicate foreign keys
In exploratory analysis, I discovered that there are duplicate foriegn keys in `df_emails` and `df_subs`.

### df_emails.cons_id
First, there are duplicate foreign keys in `df_emails.cons_id`. It *is* a possibility that `df_emails.cons_id` to `df_info.cons_id` is a one to many relationship, although unlikely due to there being two datetimes values in each row. 

**Note**: Because analysis shows that 86% of `df_emails` contains duplicate foreign keys, I opt to keep the the duplicates of `df_emails.cons_id` rather than lose valuable data. **This decision will affect the acquisition_facts.csv output**. In the case that the duplicate `df_emails.cons_id` foreign keys _should_ be removed, I left a commented function to remove the duplicate keys.

### df_subs.cons_email_ids
Additionally, there are duplicate foreign keys in `df_subs.cons_email_ids`. For this analysis, I remove the rows with duplicate `cons_email_ids` foreign keys. I remove the duplicate keys to avoid erroneously providing incorrect information on the `inunsub` status of Constituents. Sending emails to unsubscribed Constituents may run into legal issues under the CAN-SPAM Act. 

*Note*: further analysis may explore if rows with duplicate `cons_email_id` contain identical information (i.e., `isunsub`). If so, analysis can keep one instance of each duplicate.
