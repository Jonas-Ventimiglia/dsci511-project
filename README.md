# dsci511-project
Final Project by Group 5

By Stefanie Jackson, Jonas Ventimiglia and Jin Ting Zhao

**Last Run/Code update:** November 2025

## Data/Code Use and Availability
Since all data is accessible through publicly available api's, a copy of the latest run's code and output is available for public use.

## Code Layout
### Step 1: CMS Hospital Data

Use API request call using the request library to get more information on the total count and result for number of rows per page. The CMS data includes a data dictionary on the website (https://data.cms.gov/provider-data/dataset/77hc-ibv8#data-dictionary) which explains all the fields and columns and acronyms in the dataset.

Max number of rows of results from one API call is 1500.This is a sample of the CMS dataset we will be using.

### Step 2: Census Data API


### Step 3: Geocoding API

Code below demonstrates taking an address (which will come from the CMS file) and useing the CMS Geocoder to return back a GeoID. The GeoID contains the State (first 2 digits), County (digits 3-5), census tracts(digits 6-12) and block group (13-15). By using the first three components (State, County, census tract) we can connect the hospital files with the economic census files.


## Final Output

Creates a CSV called 'final_df.csv' with the following layout:

 #   Column                Non-Null Count  Dtype  
---  ------                --------------  -----  
 0   facility_id           189 non-null    object 
 1   facility_name         189 non-null    object 
 2   street                189 non-null    object 
 3   city                  189 non-null    object 
 4   state                 189 non-null    object 
 5   zip_code              189 non-null    int64  
 6   county                189 non-null    object 
 7   telephone_number      189 non-null    object 
 8   start_date            189 non-null    object 
 9   end_date              189 non-null    object 
 10  cauti_sir             189 non-null    object 
 11  cauti_lcl             189 non-null    object 
 12  cauti_catheter_days   189 non-null    object 
 13  cauti_observed        189 non-null    object 
 14  cauti_predicted       189 non-null    object 
 15  cauti_ucl             189 non-null    object 
 16  clabsi_sir            189 non-null    object 
 17  clabsi_lcl            189 non-null    object 
 18  clabsi_observed       189 non-null    object 
 19  clabsi_predicted      189 non-null    object 
 20  clabsi_ucl            189 non-null    object 
 21  clabsi_device_days    189 non-null    object 
 22  cdiff_sir             189 non-null    object 
 23  cdiff_lcl             189 non-null    object 
 24  cdiff_observed        189 non-null    object 
 25  cdiff_patient_days    189 non-null    object 
 26  cdiff_predicted       189 non-null    object 
 27  cdiff_ucl             189 non-null    object 
 28  mrsa_sir              189 non-null    object 
 29  mrsa_lcl              189 non-null    object 
 30  mrsa_observed         189 non-null    object 
 31  mrsa_patient_days     189 non-null    object 
 32  mrsa_predicted        189 non-null    object 
 33  mrsa_ucl              189 non-null    object 
 34  ssi_hyst_sir          189 non-null    object 
 35  ssi_hyst_lcl          189 non-null    object 
 36  ssi_hyst_procedures   189 non-null    object 
 37  ssi_hyst_observed     189 non-null    object 
 38  ssi_hyst_predicted    189 non-null    object 
 39  ssi_hyst_ucl          189 non-null    object 
 40  ssi_colon_sir         189 non-null    object 
 41  ssi_colon_lcl         189 non-null    object 
 42  ssi_colon_procedures  189 non-null    object 
 43  ssi_colon_observed    189 non-null    object 
 44  ssi_colon_predicted   189 non-null    object 
 45  ssi_colon_ucl         189 non-null    object 
 46  median_income         189 non-null    object 
 47  poverty_percentage    189 non-null    object 
 48  tract                 189 non-null    object 
 49  x-coordinates         189 non-null    float64
 50  y-coordinates         189 non-null    float64

## Data Limitations

* Patients do not always seek care at the hospital closest to where they live. Some may travel farther for speciality care, reputation, insurance, coverage, or previous relationships with providers, which means the surrounding income level of a hospital may not fully represent the socioeconomic status of the patients being treated there.
* Our geocoding data comes from a single source: the U.S. Census Bureaus Master Address File/Topologically Integrated Geographic Encoding and Referencing (MAF/TIGER) System. While geocoding accuracy can vary depending on the underlying data source, we expect minimal bias. Because the MAF/TIGER database reflects a specific point in time some degree of inaccuracy may occur if address information has changed since the data were compiled.
* For the CMS data, there is a limitation on the the amount of data we can query (max row of 1500) in a single call, so multiple API calls will need to be done to get all the rows in the dataset.
* Socioeconomic indicators such as income or provery rate are used as proxies for disadvantage but do not capture other important factors such as housing stability, language barriers, transportation access, or staffing shortages with the hospital.
* We had to select a single level of geographical region to link this data: census tract. While we feel that census tract balances the size of the region around the hospital, this choice may bias results compared to if we chose a smaller region (census block) or a larger region (ZCTA)
