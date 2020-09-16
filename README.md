# ALS_DataEngineer_Assessment
ALS Hiring Data Engineer Extract Transform (ETL) exercuse to manipulate and aggregate large datasets with pandas.

- [ALS_DataEngineer_Assessment](#als_dataengineer_assessment)
  - [Download](#download)
  - [Using etl_jupyternb.ipynb](#using-etl_jupyternbipynb)
  - [Using etl_script.py](#using-etl_scriptpy)
  - [Requirements](#requirements)
  - [Install Dependencies](#install-dependencies)
  - [Run script](#run-script)


There are two files to run the ETL:
  1. **etl_jupyternb.ipynb**: a [jupyter notebooks](https://github.com/jupyter/notebook) that contains all documentation, additional exploratory data analysis, and produces the output files.
  2. **etl_script.py**: python script that can be run via the terminal to produce the output files.


## Download 
This repository can be downloaded from GitHub via:

```
git clone https://github.com/{}/ALS_Assessment.git
```
*Note: removed owner name for anonymity.*


## Using etl_jupyternb.ipynb
If you have Jupyter Notebooks installed, you can access the **etl_jupyternb.ipynb** locally. Otherwise, [NBViewer.org](http://nbviewer.org) renders a GitHub Jupyter Notebook online. 
<!-- You can access the notebook online [here](https://github.com/jaimiles23/ALS_Assessment/blob/master/etl_jupyternb.ipynb) -->


## Using etl_script.py
_Note:_ This section assumes you are using Windows OS.


## Requirements
Python version 3.6+

3rd party libraries documented in requirements.txt
- numpy
- matplotlib
- pandas 
- seaborn
- missingno
- pywrangle


## Install Dependencies
To run this script, you must install the dependencies outlined in the requirements.txt file. I recommend using a virtual environment to manage these dependencies. Learn more [here](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

To install the dependencies with a virtual environment, navigate to the directory for the cloned repository and run 
```
python3 -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
deactivate
```

## Run script
After the dependencies have been installed, you can run the the etl_script.py from the command line using:

```
venv\Scripts\active
python etl_script.py
deactivate
```

NOTE:
- Activate the virtual environment to use the installed libraries
- Exclude the -m module command to run the script. 

