Full SQL tast and explanation can be found in .txt file.

1. Profile the data by finding the total number of records for each of the tables below:

SQL code:

SELECT *
From table_name;

2. Find the total distinct records by either the foreign key or primary key for each table. 	

SQL Code:

SELECT count(distinct key_name)
From table_name;

3. Are there any columns with null values in the Users table? 
Indicate "yes," or "no."
	
	SQL code:
	
	Select count(*)
	From user
	Where id IS NULL
	OR name IS NULL
	OR review_count IS NULL
	OR yelping_since IS NULL
	OR useful IS NULL
	OR funny IS NULL
	OR cool IS NULL
	OR fans IS NULL
	OR average_stars IS NULL
	OR compliment_hot IS NULL
	OR compliment_more IS NULL
	OR compliment_profile IS NULL
	OR compliment_cute IS NULL
	OR compliment_list IS NULL
	OR compliment_note IS NULL
	OR compliment_plain IS NULL
	OR compliment_cool IS NULL
	OR compliment_funny IS NULL
	OR compliment_writer IS NULL
	OR compliment_photos IS NULL;

	
4. For each table and column listed below, display the smallest (minimum),
 largest (maximum), and average (mean) value for the following fields:
		
SQL Code:

Select  
min(column), 
max(column),
avg(column)
From table_name;

5. List the cities with the most reviews in descending order:

	SQL code used to arrive at answer:
	
SELECT city, sum(review_count) as Total_Review_Number
FROM business
GROUP BY city
ORDER BY Total_Review_Number DESC;	

6. Find the distribution of star ratings to the business in the following cities:

i. Avon

SQL code used to arrive at answer:

Select sum(review_count), stars
From business
Where city = 'Avon'
Group by stars
Order by stars asc;

ii. Beachwood

SQL code used to arrive at answer:

Select sum(review_count), stars
From business
Where city = 'Beachwood'
Group by stars
Order by stars asc;

7. Find the top 3 users based on their total number of reviews:
		
	SQL code used to arrive at answer:
	
	Select id, name, review_count
	From user
	Order by review_count desc
	Limit 3;

8. Does posing more reviews correlate with more fans?

SQL code:
	
	Select name, review_count, fans
	From user
	Order by review_count desc
	Limit 10;
	
9. Are there more reviews with the word "love" or with the word "hate" in them?
	
	SQL code used to arrive at answer:

	Select count(*)
	From review 
	Where text like '%love%';
  
  
	Select count(*)
	From review 
	Where text like '%hate%';
	
10. Find the top 10 users with the most fans:

	SQL code used to arrive at answer:
	
	Select name, fans
	From user
	Order by fans desc
	Limit 10;
	
Part 2: Inferences and Analysis

1. Pick one city and category of your choice and group the businesses in 
that city or category by their overall star rating. 
Compare the businesses with 2-3 stars to the businesses with 4-5 
stars and answer the following questions. Include your code.

SELECT name, city, category, stars, hours, review_count, address
FROM business, category, hours
WHERE business.id = category.business_id 
and business.id = hours.business_id and city = 'Charlotte' 
and category = 'Shopping'
Group by name;
	
SELECT name, city, category, stars, hours, review_count, address
FROM business, category, hours
WHERE business.id = category.business_id 
and business.id = hours.business_id and city = 'Charlotte' 
and category = 'Electronics'
group by name;
		
2. Group business based on the ones that are open and the ones that are closed. What differences can you
 find between the ones that are still open and the ones that are closed? List at least two differences and
 the SQL code you used to arrive at your answer.
		
i. Difference 1:
         
The review count is way higher for the businesses which are still open.      
	  
ii. Difference 2:
         
Companies which are open is much more likely to be names as usefull, cool and funny.    
         
SQL code used for analysis:

SELECT
Sum(b.review_count),
count(r.useful)+ count(r.cool)+count(r.funny),
is_open
from business b INNER JOIN review r on b.id = r.id
group by b.is_open;	
	
3. For this last part of your analysis, you are going to choose the type of 
analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.

SQL code you used to create your final dataset:

SELECT name, city, stars, review_count, category
From business, category
where business.id = category.business_id
group by name
ORDER BY stars asc
LIMIT 10;
