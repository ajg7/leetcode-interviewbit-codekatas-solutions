## SQL (Leetcode)

### 1757. Recyclable and Low Fat Products

```sql
SELECT product_id
FROM Products
WHERE low_fats = 'Y' AND recyclable = 'Y';
```

### 1378. Replace Employee ID with the Unique Identifier

```sql
SELECT UNI.unique_id, E.name
FROM Employees AS E
LEFT JOIN EmployeeUNI AS UNI
ON UNI.id = E.id;
```

### 597. Friend Requests I: Overall Acceptance Rate

```sql
# Write your MySQL query statement below
SELECT
ROUND(
    IFNULL(
        (SELECT COUNT(*) FROM (SELECT DISTINCT requester_id, accepter_id FROM RequestAccepted) AS RA)
        /
        (SELECT COUNT(*) FROM (SELECT DISTINCT sender_id, send_to_id FROM FriendRequest) AS FR),
    0), 2
) AS accept_rate;
```

### 1667. Fix Names in a Table

```sql
SELECT user_id, CONCAT(UPPER(LEFT(name, 1)), LOWER(SUBSTRING(name, 2))) AS name
FROM users
ORDER BY user_id;
```

### 607. Sales Person

```sql
SELECT S.name
FROM salesperson AS S
WHERE S.sales_id NOT IN (
    SELECT O.sales_id
    FROM orders AS O
    LEFT JOIN company AS C
    ON O.com_id = C.com_id
    WHERE c.name = 'RED'
);
```

### 613. Shortest Distance in a Line

```sql
SELECT MIN(ABS(P2.x - P1.x)) AS shortest
FROM point AS P1, point AS P2
WHERE P1.x <> P2.x;
```

### 1571. Warehouse Manager

```sql
SELECT W.name AS warehouse_name, SUM(units * volume) AS volume
FROM Warehouse AS W
JOIN (SELECT product_id, Width * Length * Height AS volume
     FROM Products) AS P
USING (product_id)
GROUP BY W.name;
```

### 596. Classes More Than 5 Students

```sql
SELECT class
FROM courses
GROUP BY class
HAVING COUNT(DISTINCT student) >= 5
```

### 176. Second Highest Salary

```sql
SELECT MAX(Salary) AS SecondHighestSalary
FROM Employee
WHERE Salary < (
    SELECT MAX(Salary)
    FROM Employee
)
```

### 1729. Find Followers Count

```sql
SELECT F.user_id, COUNT(F.follower_id) AS followers_count
FROM Followers AS F
GROUP BY F.user_id
ORDER BY F.user_id;
```

### 1173. Immediate Food Delivery I

```sql
SELECT ROUND(SUM(D.order_date = D.customer_pref_delivery_date) * 100 / COUNT(D.delivery_id), 2) AS immediate_percentage
FROM Delivery AS D;
```

### 181. Employees Earning More Than Their Managers

```sql
SELECT E.name AS Employee
FROM Employee AS E
JOIN Employee AS E2
ON E.ManagerID = E2.Id
WHERE E.Salary > E2.Salary
```

### 610. Triangle Judgement

```sql
SELECT T.x, T.y, T.z,
IF(T.x + T.y > T.z AND T.y + T.z > T.x AND T.z + T.x > T.y, 'Yes', 'No') AS triangle
FROM triangle AS T
```

### 182. Duplicate Emails

```sql
SELECT P.Email
FROM Person AS P
GROUP BY P.Email
HAVING COUNT(P.Email) > 1
```

### 1303. Find the Team Size

```sql
SELECT E1.employee_id, E2.team_size
FROM Employee AS E1
JOIN (
    SELECT team_id, COUNT(1) AS team_size
    FROM Employee
    GROUP BY team_id
    ) AS E2
ON E1.team_id = E2.team_id;
```

### 1350. Students With Invalid Departments

```sql
SELECT S.id, S.name
FROM Students AS S
LEFT JOIN Departments AS D
ON D.id = S.department_id
WHERE D.name IS Null AND D.id IS NULL;
```

### 603. Consecutive Available Seats

```sql
SELECT DISTINCT C1.seat_id
FROM cinema AS C1, cinema AS C2
WHERE C1.free = 1
AND C2.free = 1
AND (C2.seat_id = C1.seat_id + 1 OR C2.seat_id = C1.seat_id -1);
```

### 1082. Sales Analysis I

```sql
SELECT S.seller_id
FROM Sales AS S
GROUP BY S.seller_id
HAVING SUM(S.price) = (
    SELECT SUM(S.price)
    FROM Sales AS S
    GROUP BY S.seller_id
    ORDER BY SUM(S.price) desc
    LIMIT 1
);
```

### 1495. Friendly Movies Streamed Last Month

```sql
SELECT DISTINCT C.title
FROM Content AS C
JOIN TVProgram AS TVP
ON TVP.content_id = C.content_id
WHERE C.content_type = 'Movies'
AND TVP.program_date BETWEEN '2020-06-01' AND '2020-06-30'
AND C.Kids_content = 'Y';
```

### 1148. Article Views I

```sql
SELECT author_id AS id
FROM Views
WHERE author_id = viewer_id
GROUP BY author_id
ORDER BY author_id;
```

### 1565. Unique Orders and Customers Per Month

```sql
SELECT LEFT(order_date, 7) AS month,
COUNT(order_id) AS order_count,
COUNT(DISTINCT customer_id) AS customer_count
FROM Orders
WHERE invoice > 20
GROUP BY LEFT(order_date, 7)
ORDER BY month;
```

### 175. Combine Two Tables

```sql
SELECT P.FirstName, P.LastName, A.City, A.State
FROM Person AS P
LEFT JOIN Address AS A
ON P.PersonId = A.PersonId
```

### 1280. Students and Examinations

```sql
SELECT stu.student_id, stu.student_name, sub.subject_name, SUM(e.subject_name IS NOT NULL) AS attended_exams
FROM Students AS stu
JOIN Subjects AS sub
LEFT JOIN Examinations AS e
ON stu.student_id = e.student_id AND sub.subject_name = e.subject_name
GROUP BY stu.student_name, sub.subject_name
ORDER BY stu.student_id, sub.subject_name
```

### 511. Game Play Analysis I

```sql
SELECT A.player_id, MIN(A.event_date) AS first_login
FROM Activity AS A
GROUP BY A.player_id;
```

### 512. Game Play Analysis II

```sql
SELECT A.player_id, A.device_id
FROM Activity AS A, (
    SELECT A2.player_id, MIN(A2.event_date) AS Min_Date
    FROM Activity AS A2
    GROUP BY A2.player_id
) AS Derived_Table
WHERE A.player_id=Derived_Table.player_id and A.event_date=Derived_Table.Min_Date
```

### 1623. All Valid Triplets That Can Represent a Country

```sql
SELECT A.student_name AS member_A, B.student_name AS member_B, C.student_name AS member_C
FROM SchoolA AS A
JOIN SchoolB AS B
ON A.student_id <> B.student_id AND A.student_name <> B.student_name
JOIN SchoolC AS C
ON A.student_id <> C.student_id AND B.student_id <> C.student_id
AND A.student_name <> C.student_name
AND B.student_name <> C.student_name;
```

### 1407. Top Travellers

```sql
SELECT name, IFNULL(SUM(distance), 0) AS travelled_distance
FROM Users as U
LEFT JOIN Rides as R
ON R.user_id = U.id
GROUP BY U.id
ORDER BY travelled_distance desc, name asc
```

### 1050. Actors and Directors Who Cooperated At Least Three Times

```sql
SELECT actor_id, director_id
FROM ActorDirector
GROUP BY actor_id, director_id
HAVING COUNT(actor_id) >= 3
```

### 197. Rising Temperature

```sql
SELECT W.id
FROM Weather as W
JOIN Weather as W2
ON DATEDIFF(W.recordDate, W2.recordDate) = 1
AND W.temperature > W2.temperature;
```

### 620. Not Boring Movies

```sql
SELECT *
FROM cinema
WHERE id % 2 != 0 and description <> 'boring'
order by rating desc;
```

### 595. Big Countries

```sql
SELECT name, population, area
FROM World
WHERE area > 3000000 or population > 25000000
```

### 1683. Invalid Tweets

```sql
SELECT T.tweet_id
FROM Tweets AS T
WHERE LENGTH(T.content) > 15;
```
