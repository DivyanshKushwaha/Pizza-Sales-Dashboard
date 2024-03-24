# <b>Road Accidents Analysis</b>

This dashboard helps in analysing Road accidents data for different variables or factors.

Since, the data is of year 2021 and 2022 so we have a good amount of data to visualize various aspects of Road accidents happened in the respective years.

<br>

### <b>About the Dataset</b>

This dataset has listed variables:

Accident_Index: Unique key identifier that ties the distinct accident.

Accident Date: Date of the accident happened.

Day_of_Week: Day of the accident.

Junction_Control: Place of the accident.

Junction_Detail: Type of the junction.

Accident_Severity: Condition of person whose accident happened.

Latitude: lattitude of the location.

Light_Conditions: Condition of the light when the accident happened.

Local_Authority_(District): Name of the area where accident happened.

Carriageway_Hazards: Any solid object in the lane of the road.

Longitude: longitude of the accident place.

Number_of_Casualties: Number of injured persons.

Number_of_Vehicles: Number of vehicles involved in the accident.

Police_Force: Information of Police of that location.

Road_Surface_Conditions: Condition of the road surface.

Road_Type: Type of the road on the basis of carriageway.

Speed_limit: Speed limit on that road.

Time: Time of the accident.

Urban_or_Rural_Area: Type of the location where the accident happened.

Weather_Conditions: Weather conditions when accident happened.

Vehicle_Type: Type of the vehicle of which accident happened.

<br>


### <b>Problem Statement</b>


We want to explore the dataset by various distributions on the basis of different variables and find listed distribution:

- Accident Severity Distribution

- Number of Accidents Over Time

- Distribution of Accidents by Day of the Week

- Top Junction Controls Contributing to Accidents

- Weather Conditions vs. Accident Severity

- Road Surface Conditions vs. Accident Severity


### <b>Steps Followed</b>

#### <b>1. Data Exploring and Cleaning</b>

- Imported the Dataset into the PowerBI and checked if there is missing data or duplicate data is present.
- Found that there are 3 null values in 'Carriageway_Hazards' and 17 null values in 'Time' column.
- Filled null values with 'None' in 'Carriageway_Hazards' and mode of the time in the column.
- These tasks are done in PowerBi with replace value option in transform data page.

#### <b>2. Exploratory Data Analysis</b>

- Understood various trends and distribution within the data in the PowerBi using python script.
- Also derived the Correlation Matrix among variables.
  
Here are some trends and patterns: 

#### <b>-  Accidents by Month</b>

![month](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/6b05b97d-20f2-4e71-a29c-42deb7816b93)

#### <b>-  Total Accidents by Weather Conditions</b>

![weather](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/d373d698-caf1-4dfd-a13a-3bb1009003f9)


#### <b>-  Total Accidents by Year</b>

![year](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/4767bf76-1c8a-42d8-8b50-2c4ed8bc2615)

#### <b>-  Accidents by Speed Limit</b>
![speed ;imit](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/fadfd98c-ffa3-41ba-a0fc-ac416788305e)

#### <b>-  Correlation Matrix of Variables</b>

![correlation](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/f8496e1d-5b70-47a3-b4de-8489f8ba1d67)

#### <b>3. Key Finding</b>


- To get the Month, Month Number and Year, we created Calendar Table having minimum and maximum date as the Dataset have:

          Calendar = CALENDAR(MIN(Data[Accident Date]), MAX(Data[Accident Date]))
- Then we created Columns:
    -  Month

            Month = FORMAT('Calendar'[Date],"mmm")
    - Month Number

          Month Number = MONTH('Calendar'[Date])

    - Year

          Year = YEAR('Calendar'[Date])

              
      
              
  
- To draw various distributions, we derived some measures and new columns in the PowerBi using DAX (Data Analysis Expression).

  1. Total Accidents

           Total Accidents = COUNT(Data[Accident_Index])           

  2. Day Number (Starts from Sunday)

           Day Number = WEEKDAY(Data[Accident Date],2)

  3. Current Year Accidents and Previous year Accidents for Rate of Accidents Year on Year

         CY Accidents = TOTALYTD(COUNT(Data[Accident_Index]),'Calendar'[Date])
         PY Accidents = CALCULATE(COUNT(Data[Accident_Index]), SAMEPERIODLASTYEAR('Calendar'[Date]))

  4. YoY (Year on Year) Accidents (in %)

          YoY Accidents = ([CY Accidents]-[PY Accidents])/[PY Accidents]

#### <b>4. Insights</b>
- Number Insights:
  - Total Accidents in Year 2021 and 2022 : 307.97K
  - Year on Year growth of accidents: -11.7% ( Negative sign means no. of Accidents are reduced)
  - Accidents in Year 2021: 163.55K 
  - Accidents in Year 2021: 144.42K
  - Fatal Accidents: 3.95K   ( YoY : -35.6% )
  - Serious Accidents: 40.74K  ( YoY : -14.5% )
  - Slight Accidents:  263.28K ( YoY : -10.8% )
 
- Charts Insights:
  - Most accidents happened on Friday : 50.5K
  - November 2021 has most accidents number : 15473 and most accidental Month in both years.
  - Most accidents are slight sever: 263.3K
  - Uncontrolled / Give away Junction control contributes in accidents : 150045
  - Car vehicle type causes most accidents: 245337, on second there is bike vehicle type: 25132
  - Most of the accidents happened in fine weather: 247644
  - Most accidents happens when the speed limit is 30 km/h.


