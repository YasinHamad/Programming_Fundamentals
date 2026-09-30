# Relational Diagrams Projects  
  
Process of creating ER diagram - Steps to create ERD:  
1. Entity Identification.  
2. Relationship Identification. Among all entities.  
3. Cardinality Identification. In each relationship.  
4. Identity Attributes.  
5. Create ERD.  
6. Look for Generalizations and edit if any.  
  
Process of converting ER to Tables:  
- Convert each entity to table.  
- Start dealing with relations.  
- At the end, see if you need to add any fields to the tables.  
## Simple clinic Project  
- There are a lot of acceptable solutions for the database projects. But, we have solutions that are better than other solutions.  
- When creating the database, your decision of choosing `NULL` or `NOT NULL` depends on whether the relation is "one and only one", or "one or zero".  
- Differences:  
	- He make a `Person` table.  
	- Using the `Appiontment` table, you can get the `Patient Doctor` form some `Medical Record`, so, you don't need to include them as foreign keys in the `Medical Record` table. I make the same thing for the `Payment` table for the `PatientID`.  
	- I don't think that it might happen to have a `Prescription` that doesn't belong to any `Medical Record`.  
  
### My Solution  
![[Simple_Clinic_ERD.jpg|845]]  
  
![[Simple_Clinic_TABLES 1.jpg|842]]  
  
### Doctor Solution  
![[Pasted image 20260910201636.png|842]]  
  
## Simple Library Project  
- When you have a table that is a result of a `many-to-many` relation, don't forget to add a field for the `ID` in this table, and make the Ids of the other tables foreign keys.  
![[Pasted image 20260911004407.png|368]]  
- He added this, because, these are information that some other calculations depend on.  
 ![[Pasted image 20260911004821.png|403]]  
- This means unlimited number of chars  
![[Pasted image 20260911010229.png|408]]  
- There is a big different between the two designs (me-doctor), "we borrow the copies, not the book" and everything depend on the id of the copy. You may have 100 copies of the same book. My design is still acceptable.  
- This is de-normalization, because you can get this info from another table, but putting it here makes the search faster.  
![[Pasted image 20260911011040.png|418]]  
- I guess that I missed this, it's important, in my system, I could put it in the `Payment` table.  
![[Pasted image 20260911011758.png|420]]  
  
### My Solution  
![[Simple_Library_ERD.jpg|725]]  
  
![[Simple_Library_TABLES.jpg|732]]  
  
### Doctor Solution  
![[Doctor_Solution_Library.png|736]]  
  
## Karate Club Project  
  
- It feels good to name foreign keys like this: `TableNameID`.  
![[Pasted image 20260916023112.png|577]]  
- When you have a `ISA` relation, don't forget to put the IDs.  
![[Pasted image 20260916030100.png|583]]  
- I forgot to add the current belt rank to members. I can conclude it from different table. But it is faster for search to put it here. This is called Denormalization.  
![[Pasted image 20260916030243.png|467]]  
- Not each person a member and an instructor at the same time. It should be zero-or-one.  
 ![[Pasted image 20260916030617.png|514]]  
- I should be careful next time when choosing between "zero or many" and "one or many".  
![[Pasted image 20260916032112.png|548]]  
Like this also, when adding a member, they should have a subscription.  
![[Pasted image 20260916032248.png]]  
- (Red) Instead of doing this, you can put the payment id in the two tables as foreign key.  
- (Green) A payment can't be a `BeltRankTest` and a `SubscriptionPeriod` at the same time.  
![[Pasted image 20260916032621.png|669]]  
- I can get the member id using joins, but, putting it here helps the search queries.  
-![[Pasted image 20260916034703.png|684]]  
  
### My solution  
![[Karate_Club_ERD.jpg|1105]]  
  
![[Karate_Club_TABLES.jpg|1123]]  
  
### Doctor solution  
![[Doctor_Karate_Club.png|1107]]  
  
## Car Rental Project  
- Denormalization. We can get this info form another table, but it helps for search.  
![[Pasted image 20260917023105.png|472]]  
- (Red) We calculate the value from the `StartDate EndDate` values.  
- (Green) We calculate the value using the `InitialRentalDays` and the `RentalRates` of the vehicle, which is the cost of the vehicle per day.  
![[Pasted image 20260917024550.png|466]]  
- You might say, I can get the value form the Vehicle table, no need to duplicate the value in the Rental Booking table. We duplicated the value because it might change in the future. So we need to log the value when the vehicle rented.  
![[Pasted image 20260917025027.png|701]]  
- I notice these are important, I could add them in the Payment table. The date of each payment, and the last edit date.  
![[Pasted image 20260917030111.png|612]]  
This is the final amount the customer should pay, after calculating the `AdditionalCharges` if any.  
![[Pasted image 20260917030735.png]]  
- (Red) is the mileage of the car when returned.  
- (Green) this column is computed from other fields.  
- (Black) this is the mileage this car drove. You should update this filed after the return of the car.  
![[Pasted image 20260917031057.png]]  
Note that you might not insert all data from the start, you might come back later to the row and insert additional data.  
![[Pasted image 20260917034737.png]]  
  
### My solution  
![[Car_Rental_ERD.jpg|1223]]  
  
![[Car_Rental_TABLES.png|1062]]  
  
### Doctor Solution  
![[Doctor_Car_Rental_TABLES.png|1203]]  
  
## Online Store Project  
- We will decrease this value while selling.  
![[Pasted image 20260917211938.png]]  
- Notice this attribute.  
![[Pasted image 20260917212336.png]]  
- `ContactInfro` is the email and phone for example. `LoginCredentials` is the username and password for example.  
![[Pasted image 20260917212740.png]]  
- This means that the `CustomerID` in the Orders table must be `NOT NULL`.  
![[Pasted image 20260917214017.png|739]]  
- Notice that if the primary key is the "OrderID, ProductID" and not the ID, you can't duplicate a product in the table. That might be a power point you want to use in the database.  
- I think, this is better than my design. So whenever you have a table that is a result for many-to-many relation, think if you really want the ID field or not.  
![[Pasted image 20260917223953.png|785]]  
- This is another example. A customer can add multiple reviews to the same item.  
![[Pasted image 20260917225306.png]]  
  
### My Solution  
![[Online_Store_ERD 1.jpg|982]]  
  
![[Online_Store_TABLES 1.jpg|987]]  
  
### Doctor Solution  
![[Doctor_Online_Storepng.png|1095]]  
  
---  
# What is GUID? and how to use it In Database?  
- It helps you solve some problems.  
- It stands for Global Unique Identifier.  
- It is 128 bits.  
- You can generate this GUID using any language.  
  
```sql  
select newID();  
```  
  
```sql  
select * from dbo.Sailors  
order by newID();  
-- this will return the table ordered randomly in a diff way each time you execute the query  
  
-- it is actually doing this  
select newID, * from dbo.Sailors  
order by newID();  
  
-- we have an order for the qrary proccessing  
-- not very sure about the next info  
-- it is better to do this  
-- to prevent the engine from ordering the whole table, then selecting the top 10  
select * from (select top 10 * from Employees) koko order by newID();  
-- this will select the top 10, then order them.  
```  
  
---  
# Buy and import data  
You might need to buy some data from the internet.  
You can buy up to date data.  
You can import that data as flat file. (right click on the database - tasks).  
  
How to split the big table you have into small tables?  
```sql  
-- first make the new table  
create table Body (  
	ID int identity(1,1) primary key,  
	Name nvarchar(50) not null  
);  
  
-- insert the data into it  
insert into Body  
select distinct CarDetails.Body from CarDetails;  
  
-- create a new field in the original table "ex BodyID" and make it nullable  
-- insert the IDs into it  
update CarDetails  
set BodyID = (select id from body where body.name = CarDetails.body);  
  
-- then you can make the new field in the original table, not null, and set the field as foreign key.  
```  
---  
  
# SQL Problems  
You should be able to analyze and understand the database schemas.  
  
## Explain the schema  
We can remove the green ones, because we can get them using the red one. We put them just for denormalization.  
![[Pasted image 20260924083257.png|408]]  
  
## Problem 1 - Create master view  
```sql  
-- my solution  
create view VehicleMasterDetails as   
select VehicleDetails.ID,  
	VehicleDetails.MakeID, Make = (select Makes.Make from Makes where VehicleDetails.MakeID = Makes.MakeID),  
	VehicleDetails.ModelID, ModelName = (select MakeModels.ModelName from MakeModels where VehicleDetails.ModelID = MakeModels.ModelID),  
	VehicleDetails.SubModelID, SubModelName = (select SubModels.SubModelName from SubModels where VehicleDetails.SubModelID = SubModels.SubModelID),  
	VehicleDetails.BodyID, BodyName = (select Bodies.BodyName from Bodies where VehicleDetails.BodyID = Bodies.BodyID),  
	VehicleDetails.Vehicle_Display_Name, VehicleDetails.Year,  
	DriveTypeID, DriveTypeName = (select DriveTypes.DriveTypeName from DriveTypes where VehicleDetails.DriveTypeID = DriveTypes.DriveTypeID),  
	Engine, Engine_CC, Engine_Cylinders, Engine_Liter_Display,  
	FuelTypeID, FuelTypeName = (select FuelTypes.FuelTypeName from FuelTypes where VehicleDetails.FuelTypeID = FuelTypes.FuelTypeID),  
	NumDoors  
from VehicleDetails;  
  
-- doctor solution  
-- he made a new view using the mouse :)  
```  
  
## Problem 2  
Get all vehicles made between 1950 and 2000.  
```sql  
select * from VehicleDetails where VehicleDetails.Year between 1950 and 2000;  
```  
## Problem 3  
Get number vehicles made between 1950 and 2000.  
```sql  
select count(*) as NumberOfVehicles from VehicleDetails  
where VehicleDetails.Year between 1950 and 2000;  
```  
  
## Problem 4  
Get number vehicles made between 1950 and 2000 per make and order them by Number Of Vehicles Descending  
```sql  
select Makes.Make, count(*) as NumberOfVehicles  
from VehicleDetails join Makes on VehicleDetails.MakeID = Makes.MakeID  
where VehicleDetails.Year between 1950 and 2000  
group by Makes.Make  
order by NumberOfVehicles desc;  
  
-- you can divide it into parts  
select *  
from VehicleDetails join Makes on VehicleDetails.MakeID = Makes.MakeID  
where VehicleDetails.Year between 1950 and 2000;  
  
select count(*) as NumberOfVehicles  
from VehicleDetails join Makes on VehicleDetails.MakeID = Makes.MakeID  
where VehicleDetails.Year between 1950 and 2000;  
  
select Makes.Make, count(*) as NumberOfVehicles  
from VehicleDetails join Makes on VehicleDetails.MakeID = Makes.MakeID  
where VehicleDetails.Year between 1950 and 2000  
group by Makes.Make  
order by NumberOfVehicles desc;  
```  
  
## Problem 5  
Get All Makes that have manufactured more than 12000 Vehicles in years 1950 to 2000  
  
If you want to add a condition on the result of `Group by`, always use `having`.  
`Where` is for `Select`.  
`Having` is the `Where` version for `Group by`.  
  
You can't use `Order by` in subqueries.  
  
```sql  
-- doctor solution  
select Makes.Make, count(*) as NumberOfVehicles  
from VehicleDetails join Makes on VehicleDetails.MakeID = Makes.MakeID  
where VehicleDetails.Year between 1950 and 2000  
group by Makes.Make  
having count(*) >= 12000  
order by NumberOfVehicles desc  
  
-- another solution - also my solution  
-- R1 is a table, you can use it as you want  
select * from (  
select Makes.Make, count(*) as NumberOfVehicles  
from VehicleDetails join Makes on VehicleDetails.MakeID = Makes.MakeID  
where VehicleDetails.Year between 1950 and 2000  
group by Makes.Make  
) as R1  
where NumberOfVehicles >= 12000  
order by NumberOfVehicles desc  
  
-- better version of the above solution  
select Make, NumberOfVehicles from (  
	select makeid as OriginalMakeID, count(*) as NumberOfVehicles  
	from VehicleDetails where year between 1950 and 2000  
	group by makeid  
	having count(*) >= 12000  
) as R2  
join Makes on OriginalMakeID = Makes.MakeID  
order by NumberOfVehicles desc;  
```  
  
## Problem 6  
Get number of vehicles made between 1950 and 2000 per make and add total vehicles column beside  
```sql  
select Makes.Make, count(*) as NumberOfVehicles, TotalVehicles = (select count(*) from VehicleDetails)  
from VehicleDetails join Makes on VehicleDetails.MakeID = Makes.MakeID  
where VehicleDetails.Year between 1950 and 2000  
group by Makes.Make  
order by NumberOfVehicles desc;  
```  
  
## Problem 7  
Get number of vehicles made between 1950 and 2000 per make and add total vehicles column beside it, then calculate it's percentage  
```sql  
-- my solution  
select Make, NumberOfVehicles, TotalVehicles, PercentageValue = (NumberOfVehicles * 100.0 / TotalVehicles) from (  
	select Makes.Make, count(*) as NumberOfVehicles, TotalVehicles = (select count(*) from VehicleDetails)  
	from VehicleDetails join Makes on VehicleDetails.MakeID = Makes.MakeID  
	where VehicleDetails.Year between 1950 and 2000  
	group by Makes.Make  
) as R1  
order by NumberOfVehicles desc;  
  
-- doctor solution  
select *, cast(NumberOfVehicles as float) / cast(TotalVehicles as float) as Perc from (  
	select Makes.Make, count(*) as NumberOfVehicles, TotalVehicles = (select count(*) from VehicleDetails)  
	from VehicleDetails join Makes on VehicleDetails.MakeID = Makes.MakeID  
	where VehicleDetails.Year between 1950 and 2000  
	group by Makes.Make  
) as R1  
order by NumberOfVehicles desc;  
```  
  
## Problem 8  
Get Make, FuelTypeName and Number of Vehicles per FuelType per Make  
```sql  
-- the Group by and Select statements should have the same columns  
select Makes.Make, FuelTypes.FuelTypeName, NumberOfVehicles = count(*)  
from VehicleDetails join Makes on VehicleDetails.MakeID = Makes.MakeID  
join FuelTypes on VehicleDetails.FuelTypeID = FuelTypes.FuelTypeID  
group by FuelTypeName, Make  
```  
  
## Problem 9  
Get all vehicles that runs with GAS  
```sql  
-- N is for Unicode  
select VehicleDetails.*, FuelTypes.FuelTypeName  
from VehicleDetails join FuelTypes on VehicleDetails.FuelTypeID = FuelTypes.FuelTypeID  
where FuelTypes.FuelTypeName = N'gas'  
```  
  
## Problem 10  
Get all Makes that runs with GAS  
```sql  
-- my solution  
select Makes.Make, R.FuelTypeName from (  
	select distinct MakeID, FuelTypeName  
	from VehicleDetails join FuelTypes on VehicleDetails.FuelTypeID = FuelTypes.FuelTypeID  
	where FuelTypes.FuelTypeName = N'gas'  
) as R  
join Makes on Makes.MakeID = R.MakeID  
  
-- doctor solution  
select distinct Makes.Make, FuelTypeName  
from VehicleDetails join FuelTypes on VehicleDetails.FuelTypeID = FuelTypes.FuelTypeID  
join Makes on Makes.MakeID = VehicleDetails.MakeID  
where FuelTypes.FuelTypeName = N'gas'  
```  
  
## Problem 11  
Get Total Makes that runs with GAS  
```sql  
select count(*) as TotalMakesRunOnGas from (  
	select distinct Makes.Make, FuelTypeName  
	from VehicleDetails join FuelTypes on VehicleDetails.FuelTypeID = FuelTypes.FuelTypeID  
	join Makes on Makes.MakeID = VehicleDetails.MakeID  
	where FuelTypes.FuelTypeName = N'gas'  
) as R  
```  
  
## Problem 12  
Count Vehicles by make and order them by NumberOfVehicles from high to low  
```sql  
select Make, NumberOfVehicles = count(*)  
from VehicleDetails  
join Makes on Makes.MakeID = VehicleDetails.MakeID  
group by Make  
order by NumberOfVehicles desc  
```  
  
## Problem 13  
Get all Makes/Count Of Vehicles that manufactures more than 20K Vehicles  
```sql  
select Make, NumberOfVehicles = count(*)  
from VehicleDetails  
join Makes on Makes.MakeID = VehicleDetails.MakeID  
group by Make  
having count(*) >= 20000  
order by NumberOfVehicles desc  
```  
  
## Problem 14  
Get all Makes with make starts with 'B'  
```sql  
select distinct Makes.Make  
from Makes  
where make like 'b%'  
```  
  
## Problem 15  
Get all Makes with make ends with 'W'  
```sql  
select distinct Makes.Make  
from Makes  
where make like '%w'  
```  
  
## Problem 16  
Get all Makes that manufactures DriveTypeName = FWD  
```sql  
select distinct Make, DriveTypeName  
from VehicleDetails  
join Makes on VehicleDetails.MakeID = Makes.MakeID  
join DriveTypes on VehicleDetails.DriveTypeID = DriveTypes.DriveTypeID  
where DriveTypeName = N'fwd'  
```  
  
## Problem 17  
Get total Makes that Mantufactures DriveTypeName=FWD  
```sql  
select count(*) as MakeWithFWD from (  
	select distinct Make, DriveTypeName  
	from VehicleDetails  
	join Makes on VehicleDetails.MakeID = Makes.MakeID  
	join DriveTypes on VehicleDetails.DriveTypeID = DriveTypes.DriveTypeID  
	where DriveTypeName = N'fwd'  
) as R  
```  
  
## Problem 18  
Get total vehicles per DriveTypeName Per Make and order them per make asc then per total Desc  
```sql  
-- my solution  
select Make, DriveTypeName, count(*) as NumberOfVehicles  
from VehicleDetails  
join Makes on VehicleDetails.MakeID = Makes.MakeID  
join DriveTypes on VehicleDetails.DriveTypeID = DriveTypes.DriveTypeID  
group by DriveTypeName, Make  
order by Make asc, NumberOfVehicles desc  
  
-- doctor solution  
-- idk what is the porpuse of Distinct here  
select distinct Make, DriveTypeName, count(*) as NumberOfVehicles  
from VehicleDetails  
join Makes on VehicleDetails.MakeID = Makes.MakeID  
join DriveTypes on VehicleDetails.DriveTypeID = DriveTypes.DriveTypeID  
group by DriveTypeName, Make  
order by Make asc, NumberOfVehicles desc  
```  
  
## Problem 19  
Get total vehicles per DriveTypeName Per Make then filter only results with total > 10,000  
```sql  
select Make, DriveTypeName, count(*) as NumberOfVehicles  
from VehicleDetails  
join Makes on VehicleDetails.MakeID = Makes.MakeID  
join DriveTypes on VehicleDetails.DriveTypeID = DriveTypes.DriveTypeID  
group by DriveTypeName, Make  
having count(*) >= 10000  
order by Make asc, NumberOfVehicles desc  
```  
  
## Problem 20  
Get all Vehicles that number of doors is not specified  
```sql  
select *  
from VehicleDetails  
where VehicleDetails.NumDoors is null  
```  
  
## Problem 21  
Get Total Vehicles that number of doors is not specified  
```sql  
select count(*)  
from VehicleDetails  
where VehicleDetails.NumDoors is null  
```  
  
## Problem 22  
Get percentage of vehicles that has no doors specified  
```sql  
-- my solution  
select Perc = cast(TotalVehiclesWithoutDoorsSpec as float)/cast(TotalVehicles as float) from (  
	select count(*) as TotalVehiclesWithoutDoorsSpec, TotalVehicles = (select count(*) from VehicleDetails)  
	from VehicleDetails  
	where VehicleDetails.NumDoors is null  
) as R  
  
-- doctor solution  
select (  
cast((select count(*) from VehicleDetails where NumDoors is null) as float)  
/  
cast((select count(*) from VehicleDetails) as float)  
) as Perc  
```  
  
## Problem 23  
Get MakeID , Make, SubModelName for all vehicles that have SubModelName 'Elite'  
```sql  
-- my solution  
select Makes.MakeID, Makes.Make, SubModels.SubModelName  
from VehicleDetails  
join Makes on VehicleDetails.MakeID = Makes.MakeID  
join SubModels on SubModels.ModelID = VehicleDetails.SubModelID  
where SubModelName = N'elite';  
  
-- doctor solution  
-- the only difference is Distinct  
select distinct Makes.MakeID, Makes.Make, SubModels.SubModelName  
from VehicleDetails  
join Makes on VehicleDetails.MakeID = Makes.MakeID  
join SubModels on SubModels.ModelID = VehicleDetails.SubModelID  
where SubModelName = N'elite';  
```  
  
## Problem 24  
Get all vehicles that have Engines > 3 Liters and have only 2 doors  
```sql  
select *  
from VehicleDetails  
where Engine_Liter_Display > 3 and NumDoors = 2  
```  
  
## Problem 25  
Get make and vehicles that the engine contains 'OHV' and have Cylinders = 4  
```sql  
select Makes.Make, VehicleDetails.*  
from VehicleDetails  
join Makes on Makes.MakeID = VehicleDetails.MakeID  
where Engine like '%ohv%' and Engine_Cylinders = 4  
```  
  
## Problem 26  
Get all vehicles that their body is 'Sport Utility' and Year > 2020  
```sql  
select Bodies.BodyName, VehicleDetails.*  
from VehicleDetails  
join Bodies on Bodies.BodyID = VehicleDetails.BodyID  
where Bodies.BodyName = N'sport utility' and VehicleDetails.Year > 2020  
```  
  
## Problem 27  
Get all vehicles that their Body is 'Coupe' or 'Hatchback' or 'Sedan'  
```sql  
select Bodies.BodyName, VehicleDetails.*  
from VehicleDetails  
join Bodies on Bodies.BodyID = VehicleDetails.BodyID  
where Bodies.BodyName in (N'Coupe', N'Hatchback', N'Sedan');  
```  
  
## Problem 28  
Get all vehicles that their body is 'Coupe' or 'Hatchback' or 'Sedan' and manufactured in year 2008 or 2020 or 2021  
```sql  
select Bodies.BodyName, VehicleDetails.*  
from VehicleDetails  
join Bodies on Bodies.BodyID = VehicleDetails.BodyID  
where Bodies.BodyName in (N'Coupe', N'Hatchback', N'Sedan') and VehicleDetails.Year in (2008, 2020, 2021);  
```  
  
## Problem 29  
Return found=1 if there is any vehicle made in year 1950  
```sql  
-- my solution  
select Found = 1  
where exists(select ID from VehicleDetails where VehicleDetails.Year = 1950)  
  
-- doctor solution  
select Found = 1  
where exists(select top 1 * from VehicleDetails where VehicleDetails.Year = 1950)  
```  
  
## Problem 30  
Get all Vehicle_Display_Name, NumDoors and add extra column to describe number of doors by words, and if door is null display 'Not Set'  
```sql  
select distinct Vehicle_Display_Name, NumDoors, DoorDescription =   
case  
	when NumDoors = 0 then 'Zero Doors'  
	when NumDoors = 1 then 'One Door'  
	when NumDoors = 2 then 'Two Doors'  
	when NumDoors = 3 then 'Three Doors'  
	when NumDoors = 4 then 'Four Doors'  
	when NumDoors = 5 then 'Five Doors'  
	when NumDoors = 6 then 'Six Doors'  
	when NumDoors = 8 then 'Eight Doors'  
	when NumDoors is null then 'Not Set'   
	else 'Unknown' -- in case they add another number of doors in the future  
end  
from VehicleDetails  
```  
  
## Problem 31  
Get all Vehicle_Display_Name, year and add extra column to calculate the age of the car then sort the results by age desc.  
```sql  
-- year(...) is a built in function that returns the year of the given date  
select distinct Vehicle_Display_Name, VehicleDetails.Year, Age = year(getdate()) - VehicleDetails.year  
from VehicleDetails  
order by Age desc;  
```  
  
## Problem 32  
Get all Vehicle_Display_Name, year, Age for vehicles that their age between 15 and 25 years old  
```sql  
select * from (  
	select distinct Vehicle_Display_Name, VehicleDetails.Year, Age = year(getdate()) - VehicleDetails.year  
	from VehicleDetails  
) as R  
where Age between 15 and 25  
order by Age desc;  
```  
  
## Problem 33  
Get Minimum Engine CC , Maximum Engine CC , and Average Engine CC of all Vehicles  
```sql  
select   
max(VehicleDetails.Engine_CC) as MaximumCC,  
min(VehicleDetails.Engine_CC) as MinimumCC,  
avg(VehicleDetails.Engine_CC) as AverageCC  
from VehicleDetails  
```  
  
## Problem 34  
Get all vehicles that have the minimum Engine_CC  
```sql  
select *  
from VehicleDetails  
where VehicleDetails.Engine_CC = (select min(Engine_CC) from VehicleDetails);  
```  
  
## Problem 35  
Get all vehicles that have the Maximum Engine_CC  
```sql  
select *  
from VehicleDetails  
where VehicleDetails.Engine_CC = (select max(Engine_CC) from VehicleDetails);  
```  
  
## Problem 36  
Get all vehicles that have Engin_CC below average  
```sql  
select *  
from VehicleDetails  
where VehicleDetails.Engine_CC < (select avg(Engine_CC) from VehicleDetails);  
```  
  
## Problem 37  
Get total vehicles that have Engin_CC above average  
```sql  
select count(*) as TotalVehiclesAboveAvgEngineCC from (  
	select *  
	from VehicleDetails  
	where VehicleDetails.Engine_CC > (select avg(Engine_CC) from VehicleDetails)  
) as R  
  
-- another solution  
select count(*)  
from VehicleDetails  
where VehicleDetails.Engine_CC > (select avg(Engine_CC) from VehicleDetails)  
```  
  
## Problem 38  
Get all unique Engin_CC and sort them Desc  
```sql  
select distinct Engine_CC  
from VehicleDetails  
order by Engine_CC desc  
```  
  
## Problem 39  
Get the maximum 3 Engine CC  
```sql  
select distinct top 3 Engine_CC  
from VehicleDetails  
order by Engine_CC desc  
```  
  
## Problem 40  
Get all vehicles that has one of the Max 3 Engine CC  
```sql  
select * from VehicleDetails  
where VehicleDetails.Engine_CC in   
(  
	select distinct top 3 Engine_CC  
	from VehicleDetails  
	order by Engine_CC desc  
);  
```  
  
## Problem 41  
Get all Makes that manufactures one of the Max 3 Engine CC  
```sql  
select distinct Make  
from VehicleDetails  
join Makes on Makes.MakeID = VehicleDetails.MakeID  
where VehicleDetails.Engine_CC in   
(  
	select distinct top 3 Engine_CC  
	from VehicleDetails  
	order by Engine_CC desc  
);  
```  
  
## Problem 42  
Get a table of unique Engine_CC and calculate tax per Engine CC  
```sql  
-- my solution  
select distinct Engine_CC, Tax =  
case  
	when Engine_CC between 0    and 1000 then 100  
	when Engine_CC between 1001 and 2000 then 200  
	when Engine_CC between 2001 and 4000 then 300  
	when Engine_CC between 4001 and 6000 then 400  
	when Engine_CC between 6001 and 8000 then 500  
	when Engine_CC >       8000          then 600  
	else 0  
end  
from VehicleDetails  
order by Engine_CC desc  
  
-- doctor solution  
-- this is faster than the first one. In the first one, the server computes the taxes for all rows (272869 rows) then apply the distinct.  
-- In this one, it applies the distinct first, then computes the tax for all rows (847 rows).  
select Engine_CC, Tax =  
case  
	when Engine_CC between 0    and 1000 then 100  
	when Engine_CC between 1001 and 2000 then 200  
	when Engine_CC between 2001 and 4000 then 300  
	when Engine_CC between 4001 and 6000 then 400  
	when Engine_CC between 6001 and 8000 then 500  
	when Engine_CC >       8000          then 600  
	else 0  
end  
from (select distinct VehicleDetails.Engine_CC from VehicleDetails) as R  
order by Engine_CC desc  
```  
  
## Problem 43  
Get Make and Total Number Of Doors Manufactured Per Make  
```sql  
-- my solution, I made a mistake  
select Makes.Make, count(VehicleDetails.NumDoors) as TotalNumberOfDoors from VehicleDetails  
join Makes on Makes.MakeID = VehicleDetails.MakeID  
group by Make  
order by TotalNumberOfDoors desc;  
  
-- doctor solution  
select Makes.Make, sum(VehicleDetails.NumDoors) as TotalNumberOfDoors from VehicleDetails  
join Makes on Makes.MakeID = VehicleDetails.MakeID  
group by Make  
order by TotalNumberOfDoors desc;  
```  
  
## Problem 44  
Get Total Number Of Doors Manufactured by 'Ford'  
```sql  
-- my solutions  
-- first solution and doctor solution  
select Makes.Make, sum(VehicleDetails.NumDoors) as TotalNumberOfDoors from VehicleDetails  
join Makes on Makes.MakeID = VehicleDetails.MakeID  
group by Make  
having Make = N'Ford'  
order by TotalNumberOfDoors desc;  
-- second solution  
select sum(NumDoors) as NumberOfDoorsForFord  
from VehicleDetails  
where MakeID = (select Makes.MakeID from Makes where Makes.Make = N'ford');  
  
```  
  
## Problem 45  
Get Number of Models Per Make  
```sql  
-- my solution  
-- the doctor worked on all makes, while I worked only on the makes that actually made at lease one vehicle  
select Make, count(ModelID) as TotalNumberOfModles from (  
	select distinct Makes.Make, VehicleDetails.ModelID  
	from VehicleDetails  
	join Makes on Makes.MakeID = VehicleDetails.MakeID  
) as R  
group by Make  
order by TotalNumberOfModles desc;  
  
-- doctor solution  
SELECT        Makes.Make, COUNT(*) AS NumberOfModels  
FROM            Makes INNER JOIN  
                         MakeModels ON Makes.MakeID = MakeModels.MakeID  
GROUP BY Makes.Make  
Order By NumberOfModels Desc  
```  
  
## Problem 46  
Get the highest 3 manufacturers that make the highest number of models  
```sql  
select Top 3 Makes.Make, count(ModelID) as TotalModles  
from MakeModels  
join Makes on Makes.MakeID = MakeModels.MakeID  
group by Makes.Make  
order by TotalModles desc;  
```  
  
## Problem 47  
Get the highest number of models manufactured  
```sql  
-- my solution  
select Top 1 count(ModelID) as MaxModlesManuf  
from MakeModels  
join Makes on Makes.MakeID = MakeModels.MakeID  
group by Makes.Make  
order by MaxModlesManuf desc;  
-- doctor solution  
select max(TotalModles) as MaxModlesManuf from (  
	select Makes.Make, count(ModelID) as TotalModles  
	from MakeModels  
	join Makes on Makes.MakeID = MakeModels.MakeID  
	group by Makes.Make  
) as R  
```  
  
## Problem 48  
Get the highest Manufacturers manufactured the highest number of models  
```sql  
-- my solution  
select Makes.Make, count(ModelID) as MaxModlesManuf  
from MakeModels  
join Makes on Makes.MakeID = MakeModels.MakeID  
group by Makes.Make  
having count(ModelID) = (  
	select max(TotalModles) as MaxModlesManuf from (  
		select Makes.Make, count(ModelID) as TotalModles  
		from MakeModels  
		-- I guess no need for this join, because we don't need the MakeName, the MakeID is enough  
		join Makes on Makes.MakeID = MakeModels.MakeID  
		group by Makes.Make  
	) as R  
)  
  
-- doctor solution  
SELECT        Makes.Make, COUNT(*) AS NumberOfModels  
FROM            Makes INNER JOIN  
MakeModels ON Makes.MakeID = MakeModels.MakeID  
GROUP BY Makes.Make  
having COUNT(*) = (  
	select Max(NumberOfModels) as MaxNumberOfModels  
	from  
	(  
		SELECT      MakeID, COUNT(*) AS NumberOfModels  
		FROM         
		MakeModels  
		GROUP BY MakeID  
	) R1  
)  
```  
  
## Problem 49  
Get the Lowest Manufacturers manufactured the lowest number of models  
```sql  
select Makes.Make, count(ModelID) as MaxModlesManuf  
from MakeModels  
join Makes on Makes.MakeID = MakeModels.MakeID  
group by Makes.Make  
having count(ModelID) = (  
	select min(TotalModles) as MaxModlesManuf from (  
		select MakeID, count(ModelID) as TotalModles  
		from MakeModels  
		group by MakeID  
	) as R  
)  
```  
  
## Problem 50  
Get all Fuel Types , each time the result should be showed in random order  
```sql  
-- Note that the NewID() function will generate GUID for each row  
select *   
from FuelTypes  
order by newID();  
```  
  
## Problem 51  
Get all employees that have manager along with Manager's name.  
```sql  
-- my solution  
select Employees.Name, Employees.ManagerID, Employees.Salary, R1.Name as ManagerName from Employees  
join (  
	select Employees.EmployeeID, Employees.Name from Employees  
	join (  
		select distinct ManagerID  
		from Employees  
		where ManagerID is not null  
	) as R  
	on R.ManagerID = Employees.EmployeeID  
) as R1  
on Employees.ManagerID = R1.EmployeeID  
  
-- doctor solution  
select Employees.Name, Employees.ManagerID, Employees.Salary, Managers.Name AS ManagerName   
from Employees  
join Employees as Managers on Employees.ManagerID = Managers.EmployeeID  
```  
  
## Problem 52  
Get all employees that have manager or does not have manager along with Manager's name, incase no manager name show null  
```sql  
select Employees.Name, Employees.ManagerID, Employees.Salary, Managers.Name AS ManagerName   
from Employees  
left join Employees as Managers on Employees.ManagerID = Managers.EmployeeID  
```  
  
## Problem 53  
Get all employees that have manager or does not have manager along with Manager's name, incase no manager name the same employee name as manager to himself  
```sql  
select Employees.Name, Employees.ManagerID, Employees.Salary,  
ManagerName =   
	case   
		when Managers.Name is not null then Managers.Name  
		else Employees.Name  
	end  
from Employees  
left join Employees as Managers on Employees.ManagerID = Managers.EmployeeID  
```  
  
## Problem 54  
Get All Employees managed by 'Mohammed'  
```sql  
-- my solution  
-- the only difference is the word "left join"  
select Employees.Name, Employees.ManagerID, Employees.Salary, Managers.Name AS ManagerName   
from Employees  
left join Employees as Managers on Employees.ManagerID = Managers.EmployeeID  
where Managers.Name = N'mohammed';  
  
-- doctor solution  
select Employees.Name, Employees.ManagerID, Employees.Salary, Managers.Name AS ManagerName   
from Employees  
inner join Employees as Managers on Employees.ManagerID = Managers.EmployeeID  
where Managers.Name = N'mohammed';  
```  
  
# End of course  
Always practice building queries.  
Being strong with building queries = less effort in the application = stronger developer.  
  
---  
