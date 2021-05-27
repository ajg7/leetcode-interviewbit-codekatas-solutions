# InterviewBit

## SQL (InterviewBit)

### Actors and Their Movies

```sql
SELECT M.movie_title
FROM movies AS M
RIGHT JOIN movies_cast AS MC
USING (movie_id)
WHERE MC.actor_id = (
    SELECT MC.actor_id
    FROM movies_cast AS MC
    GROUP BY MC.actor_id
    HAVING COUNT(MC.actor_id) > 1
)
```

### Short Films

```sql
SELECT m.movie_title,
    m.movie_year,
    CONCAT(director_first_name, director_last_name) AS "director_name",
    CONCAT(actor_first_name, actor_last_name) AS "actor_name",
    mc.role
FROM movies AS m
JOIN movies_cast as mc
ON mc.movie_id = m.movie_id
JOIN actors AS a
ON a.actor_id = mc.actor_id
JOIN movies_directors AS md
ON md.movie_id = m.movie_id
JOIN directors AS d
ON d.director_id = md.director_id
ORDER BY m.movie_time ASC
LIMIT 1

--I put in ASC just to remind myself of what is going on
```

### Neutral Reviewers

```sql
SELECT r.reviewer_name
FROM reviewers as r
JOIN ratings as ra
ON r.reviewer_id = ra.reviewer_id
WHERE ra.reviewer_stars IS NULL;
```

### Movie Character

```sql
SELECT CONCAT(d.director_first_name, d.director_last_name) AS director_name, m.movie_title
FROM movies AS m
JOIN movies_directors AS md
ON md.movie_id = m.movie_id
JOIN directors AS d
ON d.director_id = md.director_id
JOIN movies_cast AS mc
ON m.movie_id = mc.movie_id
WHERE mc.role = 'SeanMaguire'
```
