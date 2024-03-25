# Tidier.jl Test

# Running NPI Exploration Julia Code
You will first need to download the NPPES dataset and extract it to this directory (see step on of Programming Steps below).

In the current dirrectory, start Julia and run the following commands:
```julia
> ] # enters the package manager
> activate .
> instantiate
> # backspace to exit the package manager
> using Pluto
> Pluto.run()
```
This will open a browser window with the Pluto notebook. Open the `NPI_Exploration.jl` file and click "Run Notebook".

# Programming Specs
1) Download the most recent version of the [NPPES dataset](https://download.cms.gov/nppes/NPPES_Data_Dissemination_March_2024.zip)
2) Read it in as a Table
3) Verify NPIs with the check digit algorithm found [here](https://www.cms.gov/Regulations-and-Guidance/Administrative-Simplification/NationalProvIdentStand/Downloads/NPIcheckdigit.pdf).
4) Filter to rows that have a US state abbreviation in the `Provider Business Practice Location Address State Name` column. I am currently just checking to see if the string is two characters long.
5) Filter for active providers (`NPI Deactivation Date` is null OR `NPI Reactivation Date) is not null`)
6) Flag counseling/psychology (101Y* or 103T*), physical therapy (2251*), oncology (207RX0202X) in the `Healthcare Provider Taxonomy Code_*` columns
7) Approximate tenure of each provider by using `Provider Enumeration Date` as a proxy for the date of starting to practice
7) merge on `Estimate!!Percent!!Civilian population 18 years and over` and `Estimate!!Total!!Civilian population 18 years and over` from the 2020 ACS 5-year estimates by Practice Zip Code (`./ACSST5Y2022.S2101-Data.csv`). *Nppes data has a `Provider Business Practice Location Address Postal Code` column that can be used to merge with the ACS data*
8) Use total population to calculate the rate of each specialty group per 1,000 people in each zip code
9) Graph relationship between veteran population and specialist density
10) Graph relationship between veteran population and average specialist tenure

# Results
On my machine, the code takes about four minutes to run. This is after the notebook has been run once so all the packages are precompiled. I am happy to discuss any of the code or results with you.
