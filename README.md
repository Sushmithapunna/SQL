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






 
