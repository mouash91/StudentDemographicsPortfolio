# Student Demographics SQL Query
This SQL query provides student demographic information by retrieving data from various tables using SELECT and JOIN statements. It utilizes CASE statements for conditional logic, aggregate functions for calculations, and GROUP BY statement for data grouping. The query includes the following skills and techniques:

- SELECT statement: Retrieves specific columns and calculated values from the tables.

- JOIN statements: Utilizes INNER JOIN and LEFT OUTER JOIN to combine data from multiple tables based on specified join conditions.

- CASE statements: Performs conditional logic to convert and display values based on specific conditions.

- Aggregate function (SUM): Calculates the sum of attendance and membership days.

- Conversion functions (CAST and ROUND): Converts data types and rounds decimal values.

- GROUP BY statement: Groups data based on specified columns to perform aggregations.

***Query Explanation:***

The SQL query retrieves student demographic information and performs various transformations on the data. Here is a breakdown of the query:

- The query begins by selecting the desired columns from the student table, including endyear, personid, gender, grade, and calendarName.

- It uses a CASE statement to convert the raceEthnicityFed field from an integer data type to text and displays the corresponding race and ethnicity types.

- Another CASE statement converts the residentdistrict field from an integer data type to text and displays the top cities where students reside.

- The query includes a CASE statement to display the free/reduce lunch eligibility based on the eligibility code.

- It uses a CASE statement to convert the elstatus program status from text to a percentage.

- Another CASE statement converts the stateaid field from an integer data type to text and displays whether students are enrolling from within the resident district or outside.

- The query includes a CASE statement to display the spedstatus (special education) in percentage.

- It calculates the attendance rate by dividing the total attendance days by the total membership days and rounds the result to two decimal places. It handles a divide-by-zero error if the membership days are zero.

- The query uses table joins to collect all the demographic information from different tables, including POSEligibility, Lep, Enrollment, and v_MembershipAttendanceDetail.

- Various join conditions are used to ensure the correct data is retrieved, such as matching personID and endyear values.

- The WHERE clause filters the data to include only students enrolled in the 2022-2023 school year, active students, and specific school IDs within the district.

- The GROUP BY clause groups the data based on specified columns to perform aggregations.

***Skills Used:***

- SELECT statement: Retrieves specific columns from tables.

- JOIN statements: Combines data from multiple tables using INNER JOIN and LEFT OUTER JOIN.

- CASE statements: Performs conditional logic and converts values based on conditions.

- Aggregate function (SUM): Calculates the sum of attendance and membership days.

- Conversion functions (CAST and ROUND): Converts data types and rounds decimal values.

- GROUP BY statement: Groups data based on specified columns for aggregations.

By running this query, you can gather student demographic information, perform calculations, and obtain insights into various aspects such as race/ethnicity, residency, eligibility, special education, and attendance rate.
