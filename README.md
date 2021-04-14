# Optimal scheduling rules for elective care to minimize years of life lost during the SARS-CoV-2 pandemic

#### Project Status: In progress

## Project Description

Development of a model to optimise scheduling of elective hospital admissions in England during the COVID-19 pandemic. 

This project is a collaboration with Imperial College London and the analysis has been published as a [pre-print](https://www.imperial.ac.uk/mrc-global-infectious-disease-analysis/covid-19/report-40-hospital-scheduling/) on the website of the MRC Centre for Global Infectious Disease Analysis. The report contains a full description of the methodology. 

Please note that the code in this repository is the part of the analysis that was run by the Health Foundation. For other parts of the analysis see [add links]. 

## Outputs

## Data sources

We are using Hospital Episodes Statistics (HES) Admitted Patient Care data, covering the time period between 2015 and 2019. The NHS Digital [Data Access Request Service (DARS)](https://digital.nhs.uk/services/data-access-request-service-dars) has approved the data application for this project (DARS-NIC-276970).

Data used for this analysis were anonymised in line with the Information Commissioner's Office code of practice on anonymisation. The data were accessed in The Health Foundation's Secure Data Environment, which is a secure data analysis facility (accredited for the ISO27001 information security standard, and recognised for the NHS Digital Data Security and Protection Toolkit). No information was used that could directly identify a patient or other individual. 

## How does it work?

As the data used for this analysis is not publically available, the code cannot be used to replicate the analysis on this dataset. However, with modifications the code will be able to be used on other patient-level HES Admitted Patient Care extracts. However, once [statistical disclosure checks](https://ukdataservice.ac.uk/media/622521/thf_datareport_aw_web.pdf) have been completed, aggregate outputs of this analysis can be made available.
 

### Requirements

These scripts were written under R version version 3.6.2 (2019-12-12) -- "Dark and Stormy Night".
The following R packages (available on CRAN) are needed: 

* [**vroom**](https://cran.r-project.org/web/packages/vroom/index.html)
* [**plyr**](https://cran.r-project.org/web/packages/plyr/index.html)
* [**tidyverse**](https://www.tidyverse.org/)
* [**ggpubr**](https://cran.r-project.org/web/packages/ggpubr/index.html)
* ([**snow**](https://cran.r-project.org/web/packages/snow/index.html)
* [**lubridate**](https://cran.r-project.org/web/packages/lubridate/vignettes/lubridate.html)
* [**KFAS**](https://cran.r-project.org/web/packages/KFAS/index.html)
* [**forecast**](https://cran.r-project.org/web/packages/forecast/index.html)
* [**pryr**](https://cran.r-project.org/web/packages/pryr/index.html)
* [**stringr**](https://cran.r-project.org/web/packages/stringr/index.html)
* [**tictoc**](https://cran.r-project.org/web/packages/tictoc/index.html)
* [**foreign**](https://cran.r-project.org/web/packages/foreign/index.html)
* [**nnet**](https://cran.r-project.org/web/packages/nnet/index.html)
* [**sandwich**](https://cran.r-project.org/web/packages/sandwich/index.html) 
* [**lmtest**](https://cran.r-project.org/web/packages/lmtest/index.html)
* [**reshape2**](https://cran.r-project.org/web/packages/reshape2/index.html)
* [**DBI**](https://cran.r-project.org/web/packages/DBI/index.html)
* [**ISOweek**](https://cran.r-project.org/web/packages/ISOweek/index.html)
* [**survival**](https://cran.r-project.org/web/packages/survival/index.html)
* [**openxlsx**](https://cran.r-project.org/web/packages/openxlsx/index.html)

### Analysis code

The HES data used in this analysis was cleaned and pre-processed using our in-house [HES data pipeline](https://github.com/HFAnalyticsLab/HES_pipeline). 

The analysis was run from the script **overflow_masters.R". This script:

* Queries the SQLite database containing the HES data to extract data year by year and derives variables needed for the analysis (using functions from **prep_functions.R**)
* creates cohorts and transitions (using functions from **cohort_identification.R** and **transitions_coding.R**)
* Combines yearly transitions data into one table
* Creates a time series of the number of patients being admitted for elective and emergency care (using functions from **time_series_creator.R**)
* Creates forecasts of of the number of patients being admitted for elective and emergency care and their probability of survival(using functions from **time_series_forecast.R**)
* Runs regression models to forecast the weekly number of patients admitted to general and critical care (using functions from **regression_analyses.R**)
* Calculates average unit costs by patient group (based on age and ICD10 chapter) and waiting time quartile (using functions from **costs_merging_HF.R**)
* Creates summaries of length of stay and applies thresholds according to statistical disclosure control rules (using functions from **los_freq_tables.R** and **los_4_day_freq_tables.R**)

 
## Authors
* Josh D'Aeth - [jdaeth274](https://github.com/jdaeth274)
* Dheeya Rizmie - [dheeyarizmie](https://github.com/dheeyarizmie)
* Krystal Lau
* Fiona Grimm - [fiona-grimm](https://github.com/fiona-grimm)

## License
[to be added]
