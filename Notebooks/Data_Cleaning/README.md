# **Data Cleanup and Analysis**


## Accessing the public dataset
The raw dataset can be acquired at the following link, provided by the CDC:

COVID-19 Case Surveillance Public Use Data with Geography
https://data.cdc.gov/Case-Surveillance/COVID-19-Case-Surveillance-Public-Use-Data-with-Ge/n8mc-b4w4/data


## Filtering COVID-19 dataset down to just those related to California
The original dataset consisted of COVID-19 cases across all of the United States.
The analysis was to be focusing on cases in California, so the data was filtered down on the 'res_state' column for just 'CA'


## Removing unnecessary data
The dataset had excess columns that would not be used in our analysis.
The dataset was further slimmed down by removing the folowing unused columns:
    - state_fips_code
    - case_positive_specimen_interval
    - case_onset_interval
    - process
    - exposure_yn
    - symptom_status
    - hosp_yn
    - icu_yn
    - underlying_conditions_yn

The end result was a dataset consisting of only the following columns:
    - case_month
    - res_state
    - res_county
    - county_fips_code
    - age_group
    - sex
    - race
    - ethnicity
    - current_status
    - death_yn


## Setting consistency across NaN or missing data
The following changes were made to push more consistency across the datasets
    - 'age_group': removed "Missing" rows
    - 'sex': if "Missing" then "Unknown"
    - 'current_status': removed "Probable Cases" as we were primarily interested in lab-confirmed cases
    - 'death_yn': removed "Missing" and "Unknown" reports


## Added a new column called 'race/ethnicity' to consolidate the 'race' and 'ethnicity' columns
The following logics were applied to populate the 'race/ethnicity' column:
    - If 'race' equals "Unknown" then set 'race/ethnicity' to the value of 'ethnicity'
    - If 'race' equals "Missing" then set 'race/ethnicity' to the value of 'ethnicity'
    - If 'race/ethnicity' equals "Missing" then set 'race/ethnicity' to "Unknown"
    - If 'race' equals "White" and ethnicity equals "Hispanic/Latino" then set 'race/ethnicity' to "Hispanic/Latino"
    - Replace blanks in 'race/ethnicity' with "Unknown"
    
    
## Reorganized columns in dataset
The dataset columns were reorganized in the following sequence:
    ['year','month','case_month','res_county','res_state','county_fips_code','age_group','sex','race/ethnicity','current_status','death_yn']
    

## Cleaned dataset exported to CSV
The final cleaned dataset was exported to 'ca_data_df.csv'