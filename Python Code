#!/usr/bin/env python
# coding: utf-8

# In[1]:
# Evaluating variables: Cleaning & Manipulation 


# In[2]:
# Loading the necessary Libraries
import pandas as pd
import numpy as np


# In[3]:
# Reading Datasets Medical, Pharma and Enrollment datasets
Medical_df= pd.read_csv("C:/Users/koush/Downloads/Power BI Project/snapshot-data-medical.csv")
print('Medical:',Medical_df.head())
print("Shape:", Medical_df.shape)

Pharma_df= pd.read_csv("C:/Users/koush/Downloads/Power BI Project/snapshot-data-pharmacy.csv")
print('Pharma:',Pharma_df.head())
print("Shape:", Pharma_df.shape)

Enrollment_df= pd.read_csv("C:/Users/koush/Downloads/Power BI Project/snapshot-data-enrollment.csv")
print('Enrollment:', Enrollment_df.head())
print("Shape:", Enrollment_df.shape)


# In[4]:
# Check Duplicates:
# For the given datasets there is are no Unique ID's or Patient Identifiaction Information.
# So, to identify the duplicates we can consider a record is duplicate if all the column values matches for 2 or more records 

filter_medical = ['procedure_code','procedure_code_type','procedure_category','reporting_year','type_of_setting','payer_type','record_count']
Medical_df= Medical_df.drop_duplicates(subset= filter_medical, keep='first')
print("Shape:", Medical_df.shape)

filter_pharma= ['drug_name','reporting_year','drug_class','brand_generic','payer_type','prescription_count']
Pharma_df= Pharma_df.drop_duplicates(subset=filter_pharma, keep='first')
print("Shape:",Pharma_df.shape)

filter_enrollment= ['product_type','reporting_year','claim_type','payer_type','record_type','metric_id','metric_name','count']
Enrollment_df= Enrollment_df.drop_duplicates(subset= filter_enrollment, keep='first')
print("Shape:", Enrollment_df.shape)

# There is no duplicates found in Medical & Enrollement data but around 1k duplicates found in Pharma data.



# In[5]:
# Check Missing values: if present replacing as 'Not Known'
print('Medical_data NA: ', Medical_df.isna().sum())
print('Pharma_data NA: ', Pharma_df.isna().sum())
print('Enrollment_data NA: ', Enrollment_df.isna().sum())

# It can be seen that only Medical_data has some Null values in procedure code, so replacing them by 'Not Known'
for i,x in Medical_df['procedure_code_type'].items():
    if pd.isnull(x):
        Medical_df.loc[i, 'procedure_code_type']= 'Not Known'
        
    
# In[6]:
# Check Semicolons and Multiple values 
# Usually multiple values are sepearted by (", or ; or :"), if there are multiple values then named as 'Multiple Entries'

# Medical Data 
for col in Medical_df.columns:
    Medical_df[col] = Medical_df[col].astype(str)
    mask = Medical_df[col].str.contains(',' '|:' '|;', na=False)
    Medical_df.loc[mask, col] = 'Multiple Entries'
# Pharma Data
for col in Pharma_df.columns:
    Pharma_df[col] = Pharma_df[col].astype(str)
    mask = Pharma_df[col].str.contains(',' '|:' '|;', na=False)
    Pharma_df.loc[mask, col] = 'Multiple Entries'
# Enroll Data    
for col in Enrollment_df.columns:
    Enrollment_df[col] = Enrollment_df[col].astype(str)
    mask = Enrollment_df[col].str.contains(',' '|:' '|;', na=False)
    Enrollment_df.loc[mask, col] = 'Multiple Entries'
    

# In[7]:
# Check Outliers (outside ranges/actual list, Impossible dates)
# Identifying if year Not in 2018-2021, then replacing it by 'Incorrect Year' 
for i, x in Medical_df['reporting_year'].items():
    if str(x) not in ('2018','2019','2020','2021'):
        Medical_df.loc[i,'reporting_year'] = 'Incorrect Date'

for i, x in Pharma_df['reporting_year'].items():
    if str(x) not in ('2018','2019','2020','2021'):
        Pharma_df.loc[i,'reporting_year'] = 'Incorrect Date'
        
for i, x in Enrollment_df['reporting_year'].items():
    if str(x) not in ('2018','2019','2020','2021'):
        Enrollment_df.loc[i,'reporting_year'] = 'Incorrect Date'



# In[10]:
# Check White Spaces 
for col in Medical_df.columns:
    Medical_df[col] = Medical_df[col].astype(str).str.strip()
    
for col in Pharma_df.columns:
    Pharma_df[col] = Pharma_df[col].astype(str).str.strip()

for col in Enrollment_df.columns:
    Enrollment_df[col] = Enrollment_df[col].astype(str).str.strip()


# In[11]:
# Standardization- Captializing all the strings for easy readability and to avoid any isssues for merging if needed later

for col in Medical_df.columns:
    Medical_df[col] = Medical_df[col].astype(str).apply(lambda x: x.upper())
    
for col in Pharma_df.columns:
    Pharma_df[col] = Pharma_df[col].astype(str).apply(lambda x: x.upper())
    
for col in Enrollment_df.columns:
    Enrollment_df[col] = Enrollment_df[col].astype(str).apply(lambda x: x.upper())


# In[18]:
# Renamings/ Replaceing terms (repalcing blanks- Not Known)
# Renaming the Payer type to avoid the confusion

Medical_df= Medical_df.replace({
    'payer_type':{
    'Medi-Cal': 'Medicaid'
}})


# In[20]:
# Saving the cleaned files to local for Data Visualization 
Enrollment_df= Enrollment_df.to_csv('C:\Users\koush\Downloads\Power BI Project', index=False)

