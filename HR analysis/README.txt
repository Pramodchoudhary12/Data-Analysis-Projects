HR Analysis

--> Cleaning and Transformation using python

1) Data Type Change
   Checking for duplicates, format checking, error handling
   Merging Dataframes
   Basic analysis
2) Conditional columns
   Promotion Status = Table.AddColumn(#"Changed Type", "Custom", 
                      each if [YearsAtCompany] >= 10 then "Due For Promotion" else "Not Due For Promotion")
   Retratchment Status = Table.AddColumn(#"Renamed  
                         each if [YearsAtCompany] >= 18 then "Will Be Retreachned" else "On Service")	 	
   Distance from home  = Table.AddColumn(#"Added Conditional Column1", "Distance From Home",
                         each if [DistanceFromHome] < 10 then "Close" else if [DistanceFromHome] > 30 then "Very Far" else "Far")						 
   Job Satisfaction    = Table.AddColumn(#"Added Conditional Column4", "Job Satisfaction",
                         each if [JobSatisfaction] = 1 then "Low" else if [JobSatisfaction] > 3 then "High" else "Medium")

--> Power Bi
    Measures
	
1)	Male = CALCULATE([Total Employees],'HR-Employee-Attrition'[Gender]= "male")
2)	Female = CALCULATE([Total Employees],'HR-Employee-Attrition'[Gender]="female")
3)	Due For Promotion = CALCULATE([Total Employees],'HR-Employee-Attrition'[Promotion Status]="Due For Promotion")
4)	Not Due For Promotion = CALCULATE([Total Employees],'HR-Employee-Attrition'[Promotion Status]="Not Due For Promotion")
5)	Active Duty = CALCULATE([Total Employees],'HR-Employee-Attrition'[Retratchment Status]="On Service")
6)	Retreanch = CALCULATE([Total Employees],'HR-Employee-Attrition'[Retratchment Status]="Will Be Retreachned")
7)	Total Employees = COUNTROWS('HR-Employee-Attrition')
8)	% Female = DIVIDE([Female],[Total Employees],0)
9)	% Due For Promtion = DIVIDE([Due For Promotion],[Total Employees],0)
10)	% on service = DIVIDE([Active Duty],[Total Employees],0)
11)	% Not Due For Promotion = DIVIDE([Not Due For Promotion],[Total Employees],0)
12)	% Retreanch = DIVIDE([Retreanch],[Total Employees],0)
	
	
						 