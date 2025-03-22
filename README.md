# BIG DATA ANALYSIS

**COMPANY**: CODTECH IT SOLUTIONS

**NAME**: TANYA DEEP

**INTERN ID**: CT08WBB

**DOMAIN**: DATA ANALYSIS

**DURATION**: 4 WEEKS

**MENTOR**: NEELA SANTOSH

**DESCRIPTION**

This Python script performs a simplified air quality data analysis using Dask, demonstrating its capability to handle potentially large datasets. It begins by loading the "Air_Quality.csv" file into a Dask DataFrame and then proceeds to clean the "Data Value" column by converting it to numeric type and removing rows with missing values. The core analysis involves calculating the average "Data Value" for each "Geo Place Name" using Dask's groupby and mean functions, with the .compute() method triggering the actual distributed computation. The results are then visualized using a bar chart created with Plotly, showcasing the average air quality values across different locations. To highlight Dask's scalability, the script includes a performance comparison against Pandas. It calculates the same average values using Pandas and Dask, recording the execution time for each. This comparison demonstrates Dask's potential efficiency gains when dealing with larger datasets, as it leverages parallel processing and out-of-core computation.

Data Loading and Cleaning: Loads the CSV into a Dask DataFrame, converts the "Data Value" column to numeric, and drops rows with missing values.
Data Analysis: Calculates the average "Data Value" grouped by "Geo Place Name" using Dask.
Data Visualization: Creates a bar chart using Plotly to display the calculated averages.
Performance Comparison: Measures and prints the execution time for the same analysis performed with both Pandas and Dask, showcasing Dask's efficiency.

**Output**

Dataset Loaded Successfully!
Columns: Index(['Unique ID', 'Indicator ID', 'Name', 'Measure', 'Measure Info',
       'Geo Type Name', 'Geo Join ID', 'Geo Place Name', 'Time Period',
       'Start_Date', 'Data Value', 'Message'],
      dtype='object')

🔹 Data Value Statistics:
count    18025.000000
mean        21.428616
std         23.999345
min          0.000000
25%          8.900000
50%         15.200000
75%         26.700000
max        424.700000
Name: Data Value, dtype: float64

📈 Data Value Trend Over Years:
Start_Date
2005    41.013712
2008    20.284752
2009    26.054104
2010    27.236468
2011    15.532723
2012    25.545331
2013    19.161096
2014    16.094257
2015    21.143423
2016    18.145957
2017    20.388889
2018    15.566160
2019    24.718502
2020    14.419453
2021    14.736879
2022    14.785532
Name: Data Value, dtype: float64

🔹 Average Data Value by Measure:
Measure
Annual average concentration             2.013054
Estimated annual rate                   11.707222
Estimated annual rate (age 18+)         32.602083
Estimated annual rate (age 30+)         46.077500
Estimated annual rate (under age 18)    67.170645
Mean                                    17.234716
Million miles                           48.363759
Number per km2                          22.052431
Name: Data Value, dtype: float64

🔹 Average Data Value by Geo Place Name:
Geo Place Name
Bay Ridge and Dyker Heights (CD10)      18.738182
Bayside - Little Neck                   15.310588
Bayside Little Neck-Fresh Meadows       15.822222
Bayside and Little Neck (CD11)          17.996364
Bedford Stuyvesant (CD3)                19.417273
                                          ...    
West Queens                             19.915985
Williamsbridge and Baychester (CD12)    17.220909
Williamsburg - Bushwick                 26.159108
Willowbrook                             15.445294
Woodside and Sunnyside (CD2)            21.940909
Name: Data Value, Length: 114, dtype: float64

🔥 Worst Air Quality: High Bridge - Morrisania (38.978235294117646)

⏳ Comparing Dask vs Pandas Performance...
✅ Pandas Time: 0.09453105926513672 s
✅ Dask Time: 0.11007571220397949 s


![Image](https://github.com/user-attachments/assets/5fda758c-d16b-4f4e-9d0c-a1a121c2ec91)

![Image](https://github.com/user-attachments/assets/a5d272e7-bb62-405c-8c0b-362ac18496d5)
