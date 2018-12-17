# Creating the table in MySQL

## With the large amount of data, all queries were taking an incredible amount of time. Originally, queries were stopping because there is a built in timeout feature. I first tried editing this time limit and to find out how long a simple query would really take. After leaving the computer for 10 minutes and coming back to no results, I decided to add an index for fiscal year and agency name. With the new organization, my queries were completed in seconds. 

```SQL
USE City_Payroll_NYC;

ALTER TABLE City_Payroll_NYC.citywide_payroll_data__fiscal_year_ 
	CHANGE COLUMN `Fiscal Year` Fiscal_Year int(11)
    CHANGE COLUMN `Payroll Number` Payroll_Number text,
    CHANGE COLUMN `Agency Name` Agency_Name text,
    CHANGE COLUMN `Last Name` Last_Name text,
    CHANGE COLUMN `First Name` First_Name text,
    CHANGE COLUMN `Mid Init` Mid_Init text,
    CHANGE COLUMN `Agency Start Date` Start_Date text, 	
	CHANGE COLUMN  `Work Location Borough` Borough text,
	CHANGE COLUMN  `Title Description` Title_Description text,
	CHANGE COLUMN  `Leave Status as of June 30` Leave_Status_as_of_June30 text,
	CHANGE COLUMN  `Base Salary` Base_Salary text,
	CHANGE COLUMN  `Pay Basis` Pay_Basis text,
	CHANGE COLUMN  `Regular Hours` Regular_Hours text,
	CHANGE COLUMN  `Regular Gross Paid` Regular_Gross_Paid text,
	CHANGE COLUMN  `OT Hours` OT_Hours text,
	CHANGE COLUMN  `Total OT Paid` Total_OT_Paid text,
	CHANGE COLUMN  `Total Other Pay` Total_Other_Pay text;
    
ALTER TABLE Payroll_Data ADD INDEX (Fiscal_Year);

ALTER TABLE Payroll_Data ADD INDEX (Agency_Name);
```
## Some example queries 
```SQL
SELECT AVG(Base_Salary), Agency_Name FROM Payroll_Data
	WHERE Fiscal_Year = 2018
    GROUP BY Agency_Name;
    
SELECT Base_Salary FROM Payroll_Data
	where Last_Name = 'REED';

SELECT First_Name, Last_Name FROM Payroll_Data
	WHERE Base_Salary > 150000;    
```
