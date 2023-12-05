Part 1: Yelp Dataset Profiling and Understanding

1. Profile the data by finding the total number of records for each of the tables below:
	

	i. 	Attribute table = 10000
	ii. 	Business table = 10000
	iii. 	Category table = 10000
	iv. 	Checkin table = 10000
	v. 	elite_years table = 10000
	vi. 	friend table =  10000
	vii. 	hours table =  10000
	viii. 	photo table = 10000
	ix. 	review table = 10000
	x. 	tip table =  10000
	xi. 	user table =  10000
	
SQL code used to arrive at answer:

select count(*) as total_records
from attribute;



2. Find the total distinct records by either the foreign key or primary key for each table. If two foreign keys are listed in the table, please specify which foreign key.

i. 	Attribute table = 10000
ii. 	Business table = 10000
iii. 	Category table = 10000
iv. 	Checkin table = 10000
v. 	elite_years table = 10000
vi. 	friend table =  10000
vii. 	hours table =  10000
viii. 	photo table = 10000
ix. 	review table = 10000
x. 	tip table =  10000
xi. 	user table =  10000

Note: Primary Keys are denoted in the ER-Diagram with a yellow key icon.	

SQL code used to arrive at answer:
select count(distinct name)  + count(distinct business_id) + count(distinct value)                        
as total_records
from attribute;




3. Are there any columns with null values in the Users table? Indicate "yes," or "no."

	Answer: NO
	
	
	SQL code used to arrive at answer:
	SELECT *

FROM user

WHERE
      id IS NULL OR
      name IS NULL OR
      review_count IS NULL OR
      yelping_since IS NULL OR
      useful IS NULL OR
      funny IS NULL OR
      cool IS NULL OR
      fans IS NULL OR
      average_stars IS NULL OR
      compliment_hot IS NULL OR
      compliment_more IS NULL OR
      compliment_profile IS NULL OR
      compliment_cute IS NULL OR
      compliment_list IS NULL OR
      compliment_note IS NULL OR
      compliment_plain IS NULL OR
      compliment_cool IS NULL OR
      compliment_funny IS NULL OR
      compliment_writer IS NULL OR
      compliment_photos IS NULL
	

	
4. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:
i. Table: Review, Column: Stars

-- 		min:	1	max:	5	avg:	3.7082


-- 	ii. Table: Business, Column: Stars

-- 		min:	1	max:	5	avg:	3.6549


-- 	iii. Table: Tip, Column: Likes

-- 		min:	0	max:	2	avg: 0.0144


-- 	iv. Table: Checkin, Column: Count

-- 		min:	1	max:	53	avg:	1.9414


-- 	v. Table: User, Column: Review_count

-- 		min:	0	max:	2000	avg:	24.2995


	SQL code used to arrive at answer:
SELECT MIN(column_name)
FROM table_name;

SELECT MAX(column_name)
FROM table_name;

SELECT AVG(column_name)
FROM table_name;
 


5. List the cities with the most reviews in descending order:

	SQL code used to arrive at answer:
	SELECT city, SUM(review_count) AS 'num_of_reviews'
FROM business
GROUP BY city
ORDER BY num_of_reviews DESC;
	
	
	Copy and Paste the Result Below:
-----------------+----------------+
| city            | num_of_reviews |
+-----------------+----------------+
| Las Vegas       |          82854 |
| Phoenix         |          34503 |
| Toronto         |          24113 |
| Scottsdale      |          20614 |
| Charlotte       |          12523 |
| Henderson       |          10871 |
| Tempe           |          10504 |
| Pittsburgh      |           9798 |
| Montréal        |           9448 |
| Chandler        |           8112 |
| Mesa            |           6875 |
| Gilbert         |           6380 |
| Cleveland       |           5593 |
| Madison         |           5265 |
| Glendale        |           4406 |
| Mississauga     |           3814 |
| Edinburgh       |           2792 |
| Peoria          |           2624 |
| North Las Vegas |           2438 |
| Markham         |           2352 |
| Champaign       |           2029 |
| Stuttgart       |           1849 |
| Surprise        |           1520 |
| Lakewood        |           1465 |
| Goodyear        |           1155 |
+-----------------+----------------+
(Output limit exceeded, 25 of 362 total rows shown)

	
6. Find the distribution of star ratings to the business in the following cities:
+-------------+-------+
| Star Rating | Count |
+-------------+-------+
|         1.5 |     1 |
|         2.5 |     2 |
|         3.5 |     3 |
|         4.0 |     2 |
|         4.5 |     1 |
|         5.0 |     1 |
+-------------+-------+
i. Avon

SQL code used to arrive at answer:
SELECT stars AS 'Star Rating', COUNT(id) AS 'Count'
FROM business
WHERE city = 'Avon'
GROUP BY stars;

Copy and Paste the Resulting Table Below (2 columns â€“ star rating and count):
+-------------+-------+
| Star Rating | Count |
+-------------+-------+
|         1.5 |     1 |
|         2.5 |     2 |
|         3.5 |     3 |
|         4.0 |     2 |
|         4.5 |     1 |
|         5.0 |     1 |
+-------------+-------+

ii. Beachwood

SQL code used to arrive at answer:
SELECT stars AS 'Star Rating', COUNT(id) AS 'Count'
FROM business
WHERE city = 'Beachwood'
GROUP BY stars;


Copy and Paste the Resulting Table Below (2 columns â€“ star rating and count):
+-------------+-------+
| Star Rating | Count |
+-------------+-------+
|         2.0 |     1 |
|         2.5 |     1 |
|         3.0 |     2 |
|         3.5 |     2 |
|         4.0 |     1 |
|         4.5 |     2 |
|         5.0 |     5 |
+-------------+-------+


7. Find the top 3 users based on their total number of reviews:
		
	SQL code used to arrive at answer:
	SELECT name, review_count
FROM user
ORDER BY review_count DESC
LIMIT 3;
		
		
	Copy and Paste the Result Below:
+--------+--------------+
| name   | review_count |
+--------+--------------+
| Gerald |         2000 |
| Sara   |         1629 |
| Yuri   |         1339 |
+--------+--------------+		


8. Does posing more reviews correlate with more fans?

	Please explain your findings and interpretation of the results:
	
SELECT
	name,
	review_count,
	fans

FROM user LEFT JOIN review
ON user.id=review.user_id

ORDER BY review_count DESC
LIMIT 10

+-----------+--------------+------+
| name      | review_count | fans |
+-----------+--------------+------+
| Gerald    |         2000 |  253 |
| Sara      |         1629 |   50 |
| Yuri      |         1339 |   76 |
| .Hon      |         1246 |  101 |
| William   |         1215 |  126 |
| Harald    |         1153 |  311 |
| eric      |         1116 |   16 |
| Roanna    |         1039 |  104 |
| Mimi      |          968 |  497 |
| Christine |          930 |  173 |
+-----------+--------------+------+
ANSWER: As we can see in the table from the previous code, there are some cases when the more reviews, the more fans exist, so there is a positive correlation.Gerald, Harald and Mimi are the ones with more fans.
	
9. Are there more reviews with the word "love" or with the word "hate" in them?

	Answer:YES. There are more reviews with the word 'love' than 'hate'.
+-------------+
| COUNT(love) |
+-------------+
|        1780 |
+-------------+
	SQL code used to arrive at answer:
-- For "love" count:
SELECT COUNT(text)
FROM review
WHERE text LIKE '%love%'; 
+-------------+
| COUNT(love) |
+-------------+
|        1780 |
+-------------+

-- For "hate" count:
SELECT COUNT(text)
FROM review
WHERE text LIKE '%hate%'; 
+-------------+
| COUNT(hate) |
+-------------+
|         232 |
+-------------+
	


	
	
10. Find the top 10 users with the most fans:

	SQL code used to arrive at answer:
	SELECT name, fans
FROM user
ORDER BY fans DESC
LIMIT 10;
	
	
	Copy and Paste the Result Below:

+-----------+------+
| name      | fans |
+-----------+------+
| Amy       |  503 |
| Mimi      |  497 |
| Harald    |  311 |
| Gerald    |  253 |
| Christine |  173 |
| Lisa      |  159 |
| Cat       |  133 |
| William   |  126 |
| Fran      |  124 |
| Lissa     |  120 |
+-----------+------+

  

Part 2: Inferences and Analysis

1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.

i. Do the two groups you chose to analyze have a different distribution of hours?

Chosen city = 'Las Vegas'
Chosen category = 'Restaurants'

--First table
SELECT b.city, c.category, b.name,
    -- Categorizing based on specified stars
    CASE
        WHEN b.stars BETWEEN 2 AND 3 THEN 'Low Rating'
        WHEN b.stars BETWEEN 4 AND 5 THEN 'High Rating'
    END AS Ratings

-- Joining the business and category tables
FROM business b INNER JOIN category c 
ON b.id = c.business_id

-- Conditions for filtering and sorting
WHERE Ratings IS NOT NULL AND b.city = 'Las Vegas' AND c.category = 'Restaurants'
ORDER BY c.category;

+-----------+-------------+---------------------+-------------+
| city      | category    | name                | Ratings     |
+-----------+-------------+---------------------+-------------+
| Las Vegas | Restaurants | Wingstop            | Low Rating  |
| Las Vegas | Restaurants | Big Wong Restaurant | High Rating |
| Las Vegas | Restaurants | Jacques Cafe        | High Rating |
| Las Vegas | Restaurants | Hibachi-San         | High Rating |
+-----------+-------------+---------------------+-------------+

--2nd table: 

SELECT b.name AS 'Restaurants in Toronto', h.hours,
    -- Categorizing based on specified stars
    CASE
        WHEN b.stars BETWEEN 2 AND 3 THEN 'Low Rating'
        WHEN b.stars BETWEEN 4 AND 5 THEN 'High Rating'
    END AS Ratings

-- Joining the business and category tables
FROM (business b INNER JOIN category c) INNER JOIN hours h
ON b.id = c.business_id AND b.id = h.business_id

-- Conditions for filtering and sorting
WHERE Ratings IS NOT NULL AND c.category = 'Restaurants' AND 
    b.city = 'Las Vegas' AND Ratings = 'High Rating';
+---------+-------------+----------------------------------------+-------------+
| city    | category    | name                                   | Ratings     |
+---------+-------------+----------------------------------------+-------------+
| Phoenix | Restaurants | McDonald's                             | Low Rating  |
| Phoenix | Restaurants | Bootleggers Modern American Smokehouse | High Rating |
| Phoenix | Restaurants | Charlie D's Catfish & Chicken          | High Rating |
| Phoenix | Restaurants | Gallagher's                            | Low Rating  |
| Phoenix | Restaurants | Matt's Big Breakfast                   | High Rating |
+---------+-------------+----------------------------------------+-------------+



+--------------------------+----------------------+------------+
| Restaurants in Las Vegas | hours                | Ratings    |
+--------------------------+----------------------+------------+
| Wingstop                 | Monday|11:00-0:00    | Low Rating |
| Wingstop                 | Tuesday|11:00-0:00   | Low Rating |
| Wingstop                 | Friday|11:00-0:00    | Low Rating |
| Wingstop                 | Wednesday|11:00-0:00 | Low Rating |
| Wingstop                 | Thursday|11:00-0:00  | Low Rating |
| Wingstop                 | Sunday|11:00-0:00    | Low Rating |
| Wingstop                 | Saturday|11:00-0:00  | Low Rating |
+--------------------------+----------------------+------------+

ii. Do the two groups you chose to analyze have a different number of reviews?
         
         
iii. Are you able to infer anything from the location data provided between these two groups? Explain.

SQL code used for analysis:

		
		
2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.
		
i. Difference 1:
         
         
ii. Difference 2:
         
         
         
SQL code used for analysis:

	
	
3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.

Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:
	
i. Indicate the type of analysis you chose to do:
         
         
ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:
                           
                  
iii. Output of your finished dataset:
         
         
iv. Provide the SQL code you used to create your final dataset:
