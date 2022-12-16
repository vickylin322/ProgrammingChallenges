# SQL Challenge

The database contains two tables, store_revenue and marketing_data.  Refer to the two CSV
files, store_revenue and marketing_data to understand how these tables have been created.

store_revenue contains revenue by date, brand ID, and location:

 >  create table store_revenue (
 >     id int not null primary key auto_increment,
 >    date datetime,
 >    brand_id int,
 >    store_location varchar(250),
 >    revenue float  
 >  );

marketing_data contains ad impression and click data by date and location:

> create table marketing_data (
>  id int not null primary key auto_increment,
>  date datetime,
>  geo varchar(2),
>  impressions float,
>  clicks float
> );

### Please provide a SQL statement under each question.

* Question #0 (Already done for you as an example)
 Select the first 2 rows from the marketing data
​
>  select *
>  from marketing_data
> limit 2;
​
*  Question #1
 Generate a query to get the sum of the clicks of the marketing data
​ 
> SELECT SUM(clicks) 
> FROM marketing_data;
​
*  Question #2
 Generate a query to gather the sum of revenue by store_location from the store_revenue table
​ 
> SELECT store_location, SUM(revenue) 
> FROM store_revenue 
> GROUP BY store_location;
​
*  Question #3
 Merge these two datasets so we can see impressions, clicks, and revenue together by date
and geo.
 Please ensure all records from each table are accounted for.
​ 
> SELECT m.impression, m.clicks, SUM(s.revenue) 
> FROM marketing_data m JOIN store_revenue s
> ON m.id = s.id
> GROUP BY m.geo, m.date;
​
* Question #4
 In your opinion, what is the most efficient store and why?
In my opinion, the most efficient store would have highest revenue and highest impression. As impression means that when a user sees an advertisement. So higher number of impression indicates the marketing strategy is effective. With effetive marketing strategy, if the revenue of the store increases (in this case highest), then the store is the most efficient one. Similarly, if the marketing requires users to click (link to other websites) to indicate the users received the advertisement, then the most click marketing would lead to the most store revenue. I would like to use the ratio between impression and revenue (or ratio between clicks and revenue to measure the efficiency of the store. The highest ratio's store has the most effective marketing strategy thus most efficient. 
 
* Question #5 (Challenge)
 Generate a query to rank in order the top 10 revenue producing states
​ 
> SELECT store_location
> FROM (SELECT store_location, DENSE_RANK() OVER (ORDER BY revenue DESC) AS ranking_num FROM store_revenue)
> WHERE ranking_num <= 10;
​ 
