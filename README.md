# Dallas-Metroplext-Arrest-Sample
Sample of Dallas, Texas Arrest


-- Dallas Arrest (Sample)
use policearrest;

Select * from arrestcharges;
Select * from arrestinfo;

Select arrestNumber, ararrestdate, arlcity, cfs_number, lastname, FirstName, age, race, sex 
from arrestinfo
order by 4;

-- Highest arrest date

Select ArArrestDate as Date , count(ararrestdate) as tot_date
from arrestinfo
group by ararrestdate
order by 2 desc;

-- Highest arrests day 

Select aradow as DOW, count(ArADOW) as Tot_arrests
from arrestinfo
group by ArADOW
order by 2;


-- Arrest by Age

Select age as AGE, count(*) as Tot_Age_CT
from arrestinfo
group by age;

-- Arrest by Race

Select race as Race, count(race)  as Tot_Race
from arrestinfo
group by race;

-- Arrest by gender

Select sex, count(sex) as Tot_sex
from arrestinfo
group by sex;

-- Percentage of arrest per Race

Select race ,
count(race) as Race, count(race) *100 / 
	(select count(*) from arrestinfo) as RacePercentage
from arrestinfo
group by race
order by 3 desc;

-- Highest arrest per zipcode

Select  arlzip zip, count(Arlzip) as tot_zip
from arrestinfo
group by arlzip
order by 2 desc;

-- Percentage of arresst per zip code 

select arlzip as zip , 
count(arlzip) as tot_zip, count(arlzip) * 100 /
	(Select count(*) from arrestinfo) as ZipArrestPercentage
from arrestinfo
group by arlzip
order by ziparrestpercentage desc;


-- Age group arrested the most on a day

select age,  aradow,
	count(age)  OVER (partition by age group by aradow ) as tot_age
from arrestinfo;



Select * from arrestcharges;
Select * from arrestinfo;


-- Charges for each person 

Select arrestinfo.arrestnumber, ararrestdate, age Firstname, lastname, race, sex, arlzip,  chargeDesc, Severity 
from arrestinfo 
Join arrestcharges on  arrestcharges.ArrestNumber = arrestinfo.arrestnumber;

-- Highest charge arrest and serverity 

Select arrestinfo.arrestnumber, ChargeDesc,  count(chargeDesc) as Charge, Severity 
from arrestinfo 
Join arrestcharges on  arrestcharges.ArrestNumber = arrestinfo.arrestnumber
group by ChargeDesc
order by charge desc;

-- Total chages by zipcode 

Select arlzip, count(arlzip) as zip,  chargeDesc
from arrestinfo 
Join arrestcharges on  arrestcharges.ArrestNumber = arrestinfo.arrestnumber
group by arlzip;

--  Top 5 charges per zip code

Select arlzip as zip, count(*) as zip_charges, chargeDesc as charge
from arrestinfo 
Join arrestcharges on  arrestcharges.ArrestNumber = arrestinfo.arrestnumber
group by arlzip
order by zip_charges desc limit 5
