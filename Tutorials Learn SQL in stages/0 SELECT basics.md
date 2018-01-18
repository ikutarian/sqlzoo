## 1. Modify it to show the population of Germany

```SQL
SELECT population FROM world WHERE name= 'Germany'
```

## 2. Show the name and the population for 'Sweden', 'Norway' and 'Denmark'

```SQL
SELECT name, population FROM world WHERE name IN ('Sweden', 'Norway', 'Denmark')
```

## 3. Which countries are not too small and not too big?

```SQL
SELECT name, area FROM world WHERE area BETWEEN 200000 AND 250000
```