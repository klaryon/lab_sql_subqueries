# Lab sql subqueries
```sql
-- Setting the working database
USE sakila;

-- Write SQL queries to perform the following tasks using the Sakila database:

-- 1) Determine the number of copies of the film "Hunchback Impossible" that exist in the inventory system.   
SELECT COUNT(*) AS total_films
FROM inventory
WHERE film_id = (
    SELECT film_id
    FROM film
    WHERE title = 'Hunchback Impossible'
);

-- 2) List all films whose length is longer than the average length of all the films in the Sakila database.
SELECT title, length
FROM film 
WHERE length > (
	SELECT AVG(length) AS ave
	FROM film
);
  
-- 3) Use a subquery to display all actors who appear in the film "Alone Trip".
SELECT first_name, last_name
FROM actor AS a
WHERE actor_id IN (
    SELECT fa.actor_id
    FROM film_actor AS fa
    INNER JOIN film AS f ON fa.film_id = f.film_id
    WHERE f.title = 'Alone Trip'
);
```
