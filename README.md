# SQL
Queries
LeetCode: 
# 1173. Immediate Food Delivery I
Select Round(100*(SUM(IF(X = 'Immediate', 1, 0)))/ Count(*),2) AS Immediate_percentage 
from (Select CASE
            WHEN customer_pref_delivery_date = order_date THEN 'Immediate'
            ELSE 'Scheduled' end AS X 
            FROM Delivery AS N) 
N

# 511. Game Play Analysis I
Select player_Id, event_date as First_login
from Activity 
group by player_Id
Order by event_date ASC

# 1113: Reported Posts 
Select extra as report_reason, COUNT(DISTINCT post_id) AS report_count
FROM Actions
WHERE action_date = SUBDATE("2019-07-05", INTERVAL 1 DAY) AND extra IS NOT NULL
GROUP BY extra;

# 1148. Article Views I
Select distinct author_id as id
from Views 
where author_id = viewer_id
order by author_id ASC

# 1179. Reformat Department Table(Pivot)


# 196. Delete Duplicate Emails
Delete FROM PERSON
WHERE Id NOT IN 
(select x FROM (Select MIN(Id) as x from Person Group by Email)P)

# 197. Rising Temperature
Select Id
from ((Select Id, Temperature as t, RecordDate as d, 
    LAG(Temperature, 1) OVER(Order by RecordDate ASC) as t1,
    LAG(RecordDate,1) OVER(Order by RecordDate ASC) as d1 
from Weather)) X
where DateDiff(d,d1) = 1 AND t > t1

# 627. Swap Salary
UPDATE salary 
SET sex = case when sex = 'm' then 'f' else 'm' end

# 1211. Queries Quality and Percentage
Select query_name, 
ROUND(AVG(rating/position), 2) AS quality, 
ROUND(100*(SUM(IF((Rating < 3), 1, NULL))/Count(*)), 2) AS Poor_query_percentage 
FROM Queries
Group by query_name

# 1141. User Activity for the Past 30 Days I
Select activity_date as day, Count(distinct user_id) AS active_users
from Activity
Group by activity_date
having Datediff("2019-07-27", activity_date) < 30

# 1142. User Activity for the Past 30 Days II
Select Round(sum(a)/Sum(b),2) as average_sessions_per_user 
from (Select Round(Count(distinct session_id),2) as a, (Count(distinct user_id)) as b 
from Activity Where Datediff("2019-07-27", activity_date) < 30 Group by user_id) 
N

# 620. Not Boring Movies
Select id, movie, description, rating
from cinema 
where id % 2 != 0
AND description != 'boring'
order by rating desc

# 512. Game Play Analysis II
Select player_id, device_id
from (Select player_id, device_id, event_date, rank() Over(Partition by player_id order by event_date ASC) as Rnk from Activity)
N
where Rnk = 1
group by player_id

# 586. Customer Placing the Largest Number of Orders
Select customer_number
from (select customer_number, rank() OVER(Order by Count(Order_number) DESC) AS Rnk from Orders group by customer_number) A
where Rnk = 1

# 577. Employee Bonus
SELECT e.name, b.bonus
FROM Employee as e
LEFT JOIN bonus as b
ON e.empId = b.empId
WHERE bonus is null or bonus < 1000 

# 584. Find Customer Referee
Select name
from customer 
where COALESCE(referee_id, 0) <> 2

# 596. Classes More Than 5 Students
Select class
from courses
group by class
having count(student) >= 5

# 603. Consecutive Available Seats
select seat_id 
from cinema 
where free = 1 
AND seat_id - 1 != 0
