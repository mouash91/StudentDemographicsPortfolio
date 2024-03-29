```sql
/* Student Demographics*/

SELECT 
        s.endyear,
        s.personid,
        s.gender AS gender,
        s.grade AS grade,
        s.calendarName AS calendarname,

/*converts the "raceethnicity" field from an integer data type to text data type and then displays raceethnicity types*/

CASE 
        WHEN s.raceEthnicityFed = '1' THEN 'Hispanic'
        WHEN s.raceEthnicityFed = '2' THEN 'American Indian'
        WHEN s.raceEthnicityFed = '3' THEN 'Asian'
        WHEN s.raceEthnicityFed = '4' THEN 'Black or African American'
        WHEN s.raceEthnicityFed = '5' THEN 'Pacific Islander'
        WHEN s.raceEthnicityFed = '6' THEN 'White'
        WHEN s.raceEthnicityFed = '7' THEN 'Multiracial'
        ELSE ''
        END AS raceethnicity,

/*converts the "resident" field from an integer data type to text data type and then displays the top cities where students reside*/
	
CASE
	WHEN e.residentdistrict = '000603' THEN 'South St. Paul'
	WHEN e.residentdistrict = '019901' THEN 'Inver Grove Heights'
	WHEN e.residentdistrict = '062501' THEN 'St. Paul'
	WHEN e.residentdistrict = '083301' THEN 'South Washington'
	WHEN e.residentdistrict = '019701' THEN 'West St. Paul'
	WHEN e.residentdistrict = '019601' THEN 'Rosemount-AppleValley-Eagan'
	ELSE 'Other'
	END AS residentdistrict,

/*displays free/reduce lunch eligibility*/

CASE
	WHEN pos.eligibility = 'S' THEN 'Paid'
	WHEN pos.eligibility = 'F' THEN 'Free'
	WHEN pos.eligibility = 'R' THEN 'Reduced'
	ELSE''
	END AS freereducedeligibility,
 
/*convert text character to int and displays el status in percentage*/

CASE 
	WHEN l.programstatus = 'LEP' THEN '100.00'
	ELSE '0.00'
	END AS elstatus,

/*convert int to text and displays whether students are enrolling from within resident district our outside*/
	
CASE 
	WHEN e.stateaid = '00' THEN 'Regular'
	WHEN e.stateaid = '01' THEN 'Open Enrolled'
	ELSE 'Other'
	END AS stateaid,

/*displays sped status in percentage */

CASE
	WHEN e.specialedstatus = '4' THEN '100.00'
	ELSE '00.00'
	END AS spedstatus,

/*
The number of membership days is equivalent to the total number of school days, 
while the number of attendance days represents the number of days attended up to the current date.
*/
	
CASE
        WHEN SUM(mem.membershipdays) = 0 THEN 0 -- divide by zero error
        ELSE CAST(ROUND((SUM(mem.attendancedays) / SUM(mem.membershipdays)*100),2) as decimal(18,2))
        END AS attendancerate
    
FROM student s	

/*Using table joins to collect all demographic information*/

INNER JOIN POSEligibility pos ON s.personID = pos.personID AND pos.endyear = 2023 AND pos.enddate = '2023-06-30'
LEFT OUTER JOIN Lep l ON s.personID = l.personID
INNER JOIN Enrollment e ON s.enrollmentID = e.enrollmentID AND e.endyear = 2023 AND e.startdate <= getdate()
INNER JOIN v_MembershipAttendanceDetail mem ON s.personID = mem.personID AND mem.calendarID in (403,400,393,394,396,395,410,398,399)

WHERE s.endyear = 2023 --students enrolled in 2022-2023 school year
AND s.serviceType = 'P' --active students only
AND s.endDate IS NULL
AND schoolid IN (1,2,6,8,10,11,14,15) --all the schools within the district

GROUP BY 
        s.endyear,
        s.personid,
        s.gender,
        s.grade,
        s.calendarName,
        s.raceEthnicityFed,
        e.specialedstatus,
        e.residentDistrict,
        pos.eligibility,
        e.stateaid,
        l.programstatus
```
