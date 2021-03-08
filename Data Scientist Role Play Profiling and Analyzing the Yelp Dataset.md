Data Scientist Role Play: Profiling and Analyzing the Yelp Dataset Coursera Worksheet

This is a 2-part assignment. In the first part, you are asked a series of questions that will help you profile and understand the data just like a data scientist would. For this first part of the assignment, you will be assessed both on the correctness of your findings, as well as the code you used to arrive at your answer. You will be graded on how easy your code is to read, so remember to use proper formatting and comments where necessary.

In the second part of the assignment, you are asked to come up with your own inferences and analysis of the data for a particular research question you want to answer. You will be required to prepare the dataset for the analysis you choose to do. As with the first part, you will be graded, in part, on how easy your code is to read, so use proper formatting and comments to illustrate and communicate your intent as required.

For both parts of this assignment, use this "worksheet." It provides all the questions you are being asked, and your job will be to transfer your answers and SQL coding where indicated into this worksheet so that your peers can review your work. You should be able to use any Text Editor (Windows Notepad, Apple TextEdit, Notepad ++, Sublime Text, etc.) to copy and paste your answers. If you are going to use Word or some other page layout application, just be careful to make sure your answers and code are lined appropriately.
In this case, you may want to save as a PDF to ensure your formatting remains intact for you reviewer.



Part 1: Yelp Dataset Profiling and Understanding

1. Profile the data by finding the total number of records for each of the tables below:
	
i. Attribute table = 10000
ii. Business table = 10000
iii. Category table = 10000
iv. Checkin table = 10000
v. elite_years table = 10000
vi. friend table = 10000
vii. hours table = 10000
viii. photo table = 10000
ix. review table = 10000
x. tip table = 10000
xi. user table = 10000
	


2. Find the total distinct records by either the foreign key or primary key for each table. If two foreign keys are listed in the table, please specify which foreign key.

i. Business = 10000
ii. Hours = 1562
iii. Category = 2643
iv. Attribute = 1115
v. Review = 10000
vi. Checkin = 493
vii. Photo = 10000
viii. Tip = 537 (user_id) 3979 (business_id)
ix. User = 10000
x. Friend = 11
xi. Elite_years = 2780

Note: Primary Keys are denoted in the ER-Diagram with a yellow key icon.	



3. Are there any columns with null values in the Users table? Indicate "yes," or "no."

	Answer:

	no.
	
	SQL code used to arrive at answer:

	select *
    from user
    where name is NULL 
    or review_count is NULL 
    or yelping_since is NULL 
    or useful is NULL 
    or funny is NULL 
    or cool is NULL 
    or fans is NULL 
    or average_stars is NULL 
    or compliment_hot is NULL 
    or compliment_more is NULL 
    or compliment_profile is NULL 
    or compliment_cute is NULL 
    or compliment_list is NULL 
    or compliment_note is NULL 
    or compliment_plain is NULL 
    or compliment_cool is NULL 
    or compliment_funny is NULL 
    or compliment_writer is NULL
    or compliment_photos is NULL;
	

	
4. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:

	i. Table: Review, Column: Stars
	
		min: 1		max: 5		avg: 3.7082
		
	
	ii. Table: Business, Column: Stars
	
		min: 1		max: 5		avg: 3.6549
		
	
	iii. Table: Tip, Column: Likes
	
		min: 0		max: 2		avg: 0.0144
		
	
	iv. Table: Checkin, Column: Count
	
		min: 1		max: 53		avg: 1.9414
		
	
	v. Table: User, Column: Review_count
	
		min: 0		max: 2000	avg: 24.2995
		


5. List the cities with the most reviews in descending order:

	SQL code used to arrive at answer:
	
	select city, sum(review_count) as total_count
	from business
    group by city
	order by total_count desc;
	
	Copy and Paste the Result Below:
+-----------------+-------------+
| city            | total_count |
+-----------------+-------------+
| Las Vegas       |       82854 |
| Phoenix         |       34503 |
| Toronto         |       24113 |
| Scottsdale      |       20614 |
| Charlotte       |       12523 |
| Henderson       |       10871 |
| Tempe           |       10504 |
| Pittsburgh      |        9798 |
| Montréal        |        9448 |
| Chandler        |        8112 |
| Mesa            |        6875 |
| Gilbert         |        6380 |
| Cleveland       |        5593 |
| Madison         |        5265 |
| Glendale        |        4406 |
| Mississauga     |        3814 |
| Edinburgh       |        2792 |
| Peoria          |        2624 |
| North Las Vegas |        2438 |
| Markham         |        2352 |
| Champaign       |        2029 |
| Stuttgart       |        1849 |
| Surprise        |        1520 |
| Lakewood        |        1465 |
| Goodyear        |        1155 |
+-----------------+-------------+
(Output limit exceeded, 25 of 362 total rows shown)
	
6. Find the distribution of star ratings to the business in the following cities:

i. Avon

SQL code used to arrive at answer:

select
stars as star_rating
,sum(review_count) as count
from business
where city = 'Avon'
group by stars

Copy and Paste the Resulting Table Below (2 columns – star rating and count):

+-------------+-------+
| star_rating | count |
+-------------+-------+
|         1.5 |    10 |
|         2.5 |     6 |
|         3.5 |    88 |
|         4.0 |    21 |
|         4.5 |    31 |
|         5.0 |     3 |
+-------------+-------+

ii. Beachwood

SQL code used to arrive at answer:

select
stars as star_rating
,sum(review_count) as count
from business
where city = 'Beachwood'
group by stars

Copy and Paste the Resulting Table Below (2 columns – star rating and count):
		
+-------------+-------+
| star_rating | count |
+-------------+-------+
|         2.0 |     8 |
|         2.5 |     3 |
|         3.0 |    11 |
|         3.5 |     6 |
|         4.0 |    69 |
|         4.5 |    17 |
|         5.0 |    23 |
+-------------+-------+


7. Find the top 3 users based on their total number of reviews:
		
	SQL code used to arrive at answer:
	
	select name, review_count
	from user
	order by review_count desc
	limit 3
		
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
	
	No. We could see that from the table below.

	select name, review_count, fans
	from user
	order by review_count desc

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
| Ed        |          904 |   38 |
| Nicole    |          864 |   43 |
| Fran      |          862 |  124 |
| Mark      |          861 |  115 |
| Christina |          842 |   85 |
| Dominic   |          836 |   37 |
| Lissa     |          834 |  120 |
| Lisa      |          813 |  159 |
| Alison    |          775 |   61 |
| Sui       |          754 |   78 |
| Tim       |          702 |   35 |
| L         |          696 |   10 |
| Angela    |          694 |  101 |
| Crissy    |          676 |   25 |
| Lyn       |          675 |   45 |
+-----------+--------------+------+
	
9. Are there more reviews with the word "love" or with the word "hate" in them?

	Answer:

	yes.
	
	SQL code used to arrive at answer:

	select count(*) 
	from review
    where text like '%love%'

	select count(*) 
	from review
    where text like '%hate%'
	
10. Find the top 10 users with the most fans:

	SQL code used to arrive at answer:
	
	select name, fans
	from user
	order by fans desc
    limit 10;
	
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
	
	No. 
	There is no big difference. 
	Both of them open from Monday to Saturday, 10:00 am or 11:00 am to around 0:00 pm. 

ii. Do the two groups you chose to analyze have a different number of reviews?
    
	Yes.
	Restaurants with 3-4 stars seem to have more reviews compared with 2-3 stars ones.

iii. Are you able to infer anything from the location data provided between these two groups? Explain.
	
	Western cities like Las Vegas have the top review_count restaurants.


SQL code used for analysis:

	SELECT 
	name
	,city
	,category
	,sum(stars) sum_stars
	,review_count
	FROM business b
	INNER JOIN category c
	ON b.id = c.business_id
	GROUP BY category
	ORDER BY sum_stars DESC;
		
2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.
		
i. Difference 1:
	
	The number of Open ones far more outnumbers the closed ones.
         
ii. Difference 2:
         
    The average review_count of open ones is more than that of the closed ones.     
         
SQL code used for analysis:
	
	select is_open, count(*), avg(review_count)
	from business b
	group by is_open
	
+---------+----------+-------------------+
| is_open | count(*) | avg(review_count) |
+---------+----------+-------------------+
|       0 |     1520 |     23.1980263158 |
|       1 |     8480 |     31.7570754717 |
+---------+----------+-------------------+

3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.

Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:
	
i. Indicate the type of analysis you chose to do:

  Which category of business has the most stars in total.     
         
ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:
  
  The type of data is the sum of stars of each category, from which we could know which kind of business people like to give stars the most.
                  
iii. Output of your finished dataset:

 +---------------------------+-----------+
| category                  | sum_stars |
+---------------------------+-----------+
| Restaurants               |     245.5 |
| Shopping                  |     119.5 |
| Food                      |      87.0 |
| Health & Medical          |      69.5 |
| Nightlife                 |      69.5 |
| Home Services             |      64.0 |
| Bars                      |      59.5 |
| Beauty & Spas             |      50.5 |
| Local Services            |      50.5 |
| American (Traditional)    |      42.0 |
| Active Life               |      41.5 |
| Automotive                |      40.5 |
| Sandwiches                |      31.5 |
| Hotels & Travel           |      29.0 |
| Arts & Entertainment      |      28.0 |
| Burgers                   |      25.0 |
| Hair Salons               |      24.5 |
| Mexican                   |      24.5 |
| Event Planning & Services |      22.5 |
| Fast Food                 |      22.5 |
| Doctors                   |      21.0 |
| Bakeries                  |      20.5 |
| American (New)            |      20.0 |
| Specialty Food            |      20.0 |
| Japanese                  |      19.0 |
+---------------------------+-----------+
(Output limit exceeded, 25 of 257 total rows shown)       
         
iv. Provide the SQL code you used to create your final dataset:
	
	SELECT 
	category
	,sum(stars) sum_stars
	FROM business b
	INNER JOIN category c
	ON b.id = c.business_id
	GROUP BY category
	ORDER BY sum_stars DESC;