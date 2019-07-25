# Analysis on Medicare Provider Utilization and Payment Data: Physician and Other Supplier PUF CY2016

## Problem Statement:
* Analyze the data provided in the Medicare Data set - Medicare Provider Utilization and Payment Data: Physician and Other Supplier PUF CY2016, to provide meaningful conclusions on the Medicare data.
* Determine what factors (state, number of visits by beneficiaries, provider type, service type etc;) will impact the variances in the “Average Medicare Payment Amount”.



## Approach:

The Centers for Medicare & Medicaid Services (CMS) has prepared a public data set, the Provider Utilization and Payment Data Physician and Other Supplier Public Use File (herein referred to as “Physician and Other Supplier PUF”), with information on services and procedures provided to Medicare beneficiaries by physicians and other healthcare professionals. The Physician and Other Supplier PUF contains information on utilization, payment (allowed amount and Medicare payment), and submitted charges organized by National Provider Identifier (NPI), Healthcare Common Procedure Coding System (HCPCS) code, and place of service. This PUF is based on information from CMS administrative claims data for Medicare beneficiaries enrolled in the fee-for-service program available from the CMS Chronic Condition Data Warehouse (www.ccwdata.org). The data in the Physician and Other Supplier PUF covers calendar year 2016 and contains 100% final-action physician/supplier Part B non-institutional line items for the Medicare fee-for-service population.

Dataset details - Medicare Provider Utilization and Payment Data: Physician and Other Supplier PUF CY2016 https://data.cms.gov/Medicare-Physician-Supplier/Medicare-Provider-Utilization-and-Payment-Data-Phy/utc4-f9xp

## Data Description

'National Provider Identifier':'npi',
'Last Name/Organization Name of the Provider':'nppes_provider_last_org_name',
'First Name of the Provider':'nppes_provider_first_name',
'Middle Initial of the Provider':'nppes_provider_mi',
'Credentials of the Provider':'nppes_credentials',
'Gender of the Provider':'nppes_provider_gender',
'Entity Type of the Provider':'nppes_entity_code',
'Street Address 1 of the Provider':'nppes_provider_street1',
'Street Address 2 of the Provider':'nppes_provider_street2',
'City of the Provider':'nppes_provider_city',
'Zip Code of the Provider':'nppes_provider_zip',
'State Code of the Provider':'nppes_provider_state',
'Country Code of the Provider':'nppes_provider_country',
'Provider Type':'provider_type',
'Medicare Participation Indicator':'medicare_participation_indicator',
'Place of Service':'place_of_service',
'HCPCS Code':'hcpcs_code',
'HCPCS Description':'hcpcs_description',
'HCPCS Drug Indicator':'hcpcs_drug_indicator',
'Number of Services':'line_srvc_cnt',
'Number of Medicare Beneficiaries':'bene_unique_cnt',
'Number of Distinct Medicare Beneficiary/Per Day Services':'bene_day_srvc_cnt',
'Average Medicare Allowed Amount':'average_Medicare_allowed_amt',
'Average Submitted Charge Amount':'average_submitted_chrg_amt',
'Average Medicare Payment Amount':'average_Medicare_payment_amt',
'Average Medicare Standardized Amount':'average_Medicare_standardized_amt'

Total number of rows present in the dataset - (9714760, 26)

## Methodology


### EDA

The data has been validated for NULLs and the below listed columns were found to be having NULL values -

nppes_provider_last_org_name             136
nppes_provider_first_name             423651
nppes_provider_mi                    2760957
nppes_credentials                     668142
nppes_provider_gender                 423555
nppes_provider_street2               5529780
nppes_provider_zip                         2

Out of the NULL values shown above, per the Medicare data overview document, the below rules were to be followed while cleaning up the NULL values.

nppes_provider_last_org_name – When the provider is registered in NPPES as an individual (entity type code=’I’), this is the provider’s last name. When the provider is registered as an organization (entity type code = ‘O’), this is the organization name.

nppes_provider_first_name – When the provider is registered in NPPES as an individual (entity type code=’I’), this is the provider’s first name. When the provider is registered as an organization (entity type code = ‘O’), this will be blank.

nppes_provider_mi – When the provider is registered in NPPES as an individual (entity type code=’I’), this is the provider’s middle initial. When the provider is registered as an organization (entity type code = ‘O’), this will be blank.

nppes_provider_gender – When the provider is registered in NPPES as an individual (entity type code=’I’), this is the provider’s gender. When the provider is registered as an organization (entity type code = ‘O’), this will be blank.

nppes_credentials – When the provider is registered in NPPES as an individual (entity type code=’I’), these are the provider’s credentials. When the provider is registered as an organization (entity type code = ‘O’), this will be blank.

nppes_provider_street2 – The second line of the provider’s street address, as reported in NPPES. If null, I planned to ignore the value.

nppes_provider_zip – The provider’s zip code, as reported in NPPES. If null, I planned to remove.

Cleaning -

Remove the records where the entity type is "Individual" and has no last name listed - 136 records removed
Remove the records where the entity type is "Individual" and has no first name listed - 96 records removed
Remove the Middle name column all together, as there are 2337301 rows with no middle name, and all are Individual type.
Remove the rows where credentials were not provided - 244587 records removed
Remove the 2 records where Zip is null

If the entity is an Organization, then gender can be null; No action needed on those records
Review the Nulls again, NULLs in Street2 can be ignored


Review the shape of the dataset after removing rows/columns above -> (9470077, 25)


* ** Interesting Facts from the Medicare Payment Data **
- Number of transactions are with Medicare Participation Indicator as Y are 9466639 out of the 9470077. Only 3436 transactions were with Medicare Participation Indicator as N.

- The provider type which is most in demand with most number of transactions involved is - <b> Diagnostic Radiology </b> with 1237600 records, followed by <b> Internal Medicine </b> with 1136474 number of transactions.

- Cardiovascular Disease (Cardiology) lists fifth in position with total number of transactions - 444644

- Within the Cardiovascular Disease (Cardiology), the specific service that has most number of transactions listed is for "Established patient office or other outpatient visit, typically 15 minutes" which has 437770 records.

- Number of participants who registered as "Individual" provides - 9046520

- Number of participants who registered as "Organization" providers are - 423555

- Number of transactions listed in the State California (CA) itself - 745,000 records

## Analysis Performed

[Analysis performed on the Medicare Provider Utilization and Payment Data](/data/Medicare Provider Utilization and Payment Data.pdf)


## Sources
* This Medicare Data has been downloaded from https://data.cms.gov/Medicare-Physician-Supplier/Medicare-Provider-Utilization-and-Payment-Data-Phy/utc4-f9xp
