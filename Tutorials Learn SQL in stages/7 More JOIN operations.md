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