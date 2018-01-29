## 1. List the films where the yr is 1962 [Show id, title]

```SQL
SELECT id, title
 FROM movie
 WHERE yr=1962
```

## 2. Give year of 'Citizen Kane'

```SQL
SELECT yr
 FROM movie
 WHERE title = 'Citizen Kane'
```

## 3. List all of the Star Trek movies, include the id, title and yr (all of these movies include the words Star Trek in the title). Order results by year

```SQL
SELECT id, title, yr
 FROM movie
 WHERE title LIKE '%Star Trek%' ORDER BY yr
```

## 4. What id number does the actor 'Glenn Close' have?

```SQL
SELECT id
 FROM actor
 WHERE name = 'Glenn Close';
```

## 5. What is the id of the film 'Casablanca'

```SQL
SELECT id 
 FROM movie 
 WHERE title = 'Casablanca'
```

## 6. Obtain the cast list for 'Casablanca'.

```SQL
SELECT actor.name 
 FROM actor 
 JOIN casting ON casting.movieid = 11768 
 WHERE casting.actorid = actor.id
```

## 7. Obtain the cast list for the film 'Alien'

```SQL
SELECT actor.name 
 FROM actor 
 JOIN casting ON casting.movieid = (SELECT id FROM movie WHERE title = 'Alien') 
 WHERE casting.actorid = actor.id
```

Or you can use this

```SQL
SELECT actor.name 
 FROM actor 
 JOIN casting ON casting.actorid = actor.id 
 JOIN movie ON movie.id = casting.movieid 
 WHERE movie.title = 'Alien'
```

## 8. List the films in which 'Harrison Ford' has appeared

```SQL
SELECT movie.title 
 FROM movie 
 JOIN casting ON movie.id = casting.movieid 
 JOIN actor ON actor.id = casting.actorid 
 WHERE actor.name = 'Harrison Ford'
```

## 9. List the films where 'Harrison Ford' has appeared - but not in the starring role

```SQL
SELECT movie.title
 FROM movie
 JOIN casting ON movie.id = casting.movieid
 JOIN actor ON actor.id = casting.actorid
 WHERE actor.name = 'Harrison Ford' AND casting.ord != 1
```

## 10. List the films together with the leading star for all 1962 films

```SQL
SELECT movie.title, actor.name
 FROM movie
 JOIN casting ON movie.id = casting.movieid
 JOIN actor ON actor.id = casting.actorid
 WHERE casting.ord = 1 AND movie.yr = 1962
```

## 11. Which were the busiest years for 'John Travolta', show the year and the number of movies he made each year for any year in which he made more than 2 movies

```SQL
SELECT * FROM 
  (SELECT movie.yr, COUNT(movie.yr) AS num
    FROM actor 
    JOIN casting ON casting.actorid = actor.id  
    JOIN movie ON casting.movieid = movie.id  
    WHERE actor.name = 'John Travolta'
    GROUP BY movie.yr) AS t
WHERE t.num > 2
```

## 12. List the film title and the leading actor for all of the films 'Julie Andrews' played in

```SQL
SELECT movie.title, actor.name 
 FROM movie 
 JOIN casting ON casting.movieid = movie.id AND casting.ord = 1
 JOIN actor ON actor.id = casting.actorid
 WHERE 
  casting.movieid IN (
   SELECT movieid FROM casting 
    WHERE actorid IN (SELECT id FROM actor WHERE name='Julie Andrews'))
```

## 13. Obtain a list, in alphabetical order, of actors who've had at least 30 starring roles

```SQL
SELECT actor.name
 FROM actor
 JOIN casting ON casting.actorid = actor.id 
 WHERE casting.ord = 1
 GROUP BY actor.name
 HAVING COUNT(movieid) >= 30
 ORDER BY actor.name
```

## 14. List the films released in the year 1978 ordered by the number of actors in the cast, then by title

```SQL
SELECT movie.title, COUNT(casting.actorid)
 FROM movie
 JOIN casting on casting.movieid = movie.id
 WHERE movie.yr = 1978
 GROUP BY movie.title
 ORDER BY COUNT(casting.actorid) DESC, movie.title
```

## 15. List all the people who have worked with 'Art Garfunkel'

```SQL
SELECT actor.name 
 FROM actor 
 JOIN casting ON casting.actorid = actor.id 
 WHERE casting.movieid IN (SELECT casting.movieid 
   FROM casting 
   JOIN actor ON casting.actorid = actor.id 
   WHERE actor.name = 'Art Garfunkel')
 AND actor.name <> 'Art Garfunkel'
```