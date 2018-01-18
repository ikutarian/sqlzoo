## 1. Introduction

```SQL
SELECT name, continent, population FROM world
```

## 2. Large Countries

```SQL
SELECT name FROM world WHERE population >= 200000000
```

## 3. Per capita GDP

```SQL
SELECT name, GDP/population FROM world WHERE population >= 200000000
```

## 4. South America In millions

```SQL
SELECT name, population/1000000 FROM world WHERE continent = 'South America'
```

## 5. France, Germany, Italy

```SQL
SELECT name, population FROM world WHERE name IN ('France', 'Germany', 'Italy')
```

## 6. United

```SQL
SELECT name FROM world WHERE name LIKE '%United%'
```

## 7. Two ways to be big

```SQL
SELECT name, population, area FROM world WHERE area > 3000000 OR population > 250000000
```

## 8. One or the other (but not both)

```SQL
SELECT name, population, area FROM world WHERE area > 3000000 XOR population > 250000000
```

## 9. Rounding

```SQL
SELECT name, ROUND(population /1000000, 2), ROUND(gdp /1000000000, 2) FROM world WHERE continent = 'South America'
```

## 10. Trillion dollar economies

```SQL
SELECT name, ROUND(gdp / population, -3) FROM world WHERE gdp > 1000000000000
```

## 11. Name and capital have the same length

```SQL
SELECT name, capital FROM world WHERE LENGTH(name) = LENGTH(capital)
```

## 12. Matching name and capital

```SQL
SELECT name, capital FROM world WHERE LEFT(name, 1) = LEFT(capital, 1) AND  name <> capital
```

## 13. All the vowels

```SQL
SELECT name FROM world 
WHERE
    name LIKE '%a%' 
    AND name LIKE '%e%' 
    AND name LIKE '%i%' 
    AND name LIKE '%o%'
    AND name LIKE '%u%' 
    AND name 
    NOT LIKE '% %'
```