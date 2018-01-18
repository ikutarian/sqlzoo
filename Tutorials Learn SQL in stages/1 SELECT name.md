## 1. Find the country that start with Y

```SQL
SELECT name FROM world WHERE name LIKE 'Y%'
```

## 2. Find the countries that end with y

```SQL
SELECT name FROM world WHERE name LIKE '%Y'
```

## 3. Find the countries that contain the letter x

```SQL
SELECT name FROM world WHERE name LIKE '%x%'
```

## 4. Find the countries that end with land

```SQL
SELECT name FROM world WHERE name LIKE '%land'
```

## 5. Find the countries that start with C and end with ia

```SQL
SELECT name FROM world WHERE name LIKE 'C%ia'
```

## 6. Find the country that has oo in the name

```SQL
SELECT name FROM world WHERE name LIKE '%oo%'
```

## 7. Find the countries that have three or more a in the name

```SQL
SELECT name FROM world WHERE name LIKE '%a%a%a%'
```

## 8. Find the countries that have "t" as the second character.

```SQL
SELECT name FROM world WHERE name LIKE '_t%' ORDER BY name
```