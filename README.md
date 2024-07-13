# Electric-Vehicle-Analysis
### Dashboard Link : [https://app.powerbi.com/groups/me/reports/384d017e-e935-44dc-9e7d-1626c1a36de1/ReportSection](https://app.powerbi.com/groups/me/reports/b135e483-b6f0-4f71-aeab-37094d5d9a5d/ReportSection?redirectedFromSignup=1&experience=power-bi)

### Overview :
This dashboard, titled "Drive Green: ELECTRIC VEHICLE ANALYSIS," provides a comprehensive analysis of the electric vehicle (EV) population. It offers insightful visualizations and key metrics that help understand the adoption and distribution of electric vehicles across different regions, manufacturers, and models.

### Steps followed :
#### Data Transformation:
- Step 1: Load the dataset into PowerBi Desktop. Click on 'Transform Data' to clean the dataset.
- Step 2: Change datatype of all columns based on their values in dataset.
- Step 3: Remove columns 'VIN(1-10)' and 'County'.
- Step 4: Duplicate the 'Electric Vehicle Type' column and replace value 'Battery Electric Vehicle (BEV)' to 'BEV' and 'Plug-in Hybrid Electric Vehicle (PHEV)' to 'PHEV' and rename the duplicated column to 'Electric Vehicle Type Acronym'.
- Step 5: Duplicate the 'Clean Alternative Fuel Vehicle (CAFV) Eligibility'column and replace value 'Clean Alternative Fuel Vehicle Eligible' to 'Eligible', 'Not eligible due to low battery range' to 'Not Eligible', and 'Eligibility unknown as battery range has not been researched' to 'Unknown(Battery not researched)' and rename the duplicated column to 'CAFV Check'.
- Step 6: Select 'Close & Apply' to apply the changes made.

#### Data Visualization:
- Create New Measures from following DAX script:
1. Avg Range KPI = CONCATENATE(FORMAT(AVERAGE(Electric_Vehicle_Population_Data[Electric Range]),"0.00"),"Kms")
2. BEV %age = [BEV KPI]/COUNT(Electric_Vehicle_Population_Data[DOL Vehicle ID])
3. BEV KPI = CALCULATE(COUNT(Electric_Vehicle_Population_Data[DOL Vehicle ID]), Electric_Vehicle_Population_Data[Electric Vehicle Type Acronym]="BEV")
4. PHEV %age = [PHEV KPI]/COUNT(Electric_Vehicle_Population_Data[DOL Vehicle ID])
5. PHEV KPI = CALCULATE(COUNT(Electric_Vehicle_Population_Data[DOL Vehicle ID]), Electric_Vehicle_Population_Data[Electric Vehicle Type Acronym]="PHEV")

- Create Visuals:
a. Total Vehicles -
    Card
    Fields = Count of DOL Vehicle ID
b. Average Electric Range -
    Card
    Fields = Avg Range KPI
c. Total Vehicles by Model Year (2010 onwards) -
    Area chart
    X-axis = Model Year
    Y-axis = Count of DOL Vehicle ID
    From Filters pane, select only years after 2009
d. Top 10 Total Vehicles by Model -
    Treemap
    Category = Model
    Values = Count of DOL Vehicle ID
e. Top 10 Vehicles by Make -
    Stacked bar chart
    Y-axis = Make
    X-axis = Count of DOL Vehicle ID
    From Filters pane, Apply filter to 'Make' by selecting Filter Type Top N and set value as Count of DOL Vehicle ID.
f. Vehicle by CAFV Eligibility -
    Pie chart
    Legend = CAFV Check
    Values = Count of CAFV Check
g. Total Vehicle by State -
    Shape map
    Location = State
    Color Saturation = Count of DOL Vehicle ID
h. Vehicle Type Distribution 1 -
    Donut chart
    Legend = Electric Type Vehicle Acronym
    Values = Count of Electric Type Vehicle Acronym
    (Emphasize BEV in this chart)
    Card
    Fields = BEV KPI
    Fields = BEV %age
i. Vehicle Type Distribution 2 -
    Donut chart
    Legend = Electric Type Vehicle Acronym
    Values = Count of Electric Type Vehicle Acronym
    (Emphasize PHEV in this chart)
    Card
    Fields = PHEV KPI
    Fields = PHEV %age
j. Filters -
    1. Electric Utility
    2. Make
    3. Model Year
    4. City
