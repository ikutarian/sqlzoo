## 1. Winners from 1950

```SQL
SELECT 
  yr, subject, winner 
FROM 
  nobel 
WHERE 
  yr = 1950
```

## 2. 1962 Literature

```SQL
SELECT 
  winner 
FROM 
  nobel 
WHERE 
  yr = 1962 
  AND 
  subject = 'Literature'
```

## 3. Albert Einstein

```SQL
SELECT 
  yr, subject 
FROM 
  nobel 
WHERE winner= 'Albert Einstein'
```

## 4. Recent Peace Prizes

```SQL
SELECT 
  winner 
FROM 
  nobel 
WHERE 
  yr >= 2000 AND subject = 'Peace'
```

## 5. Literature in the 1980's

```SQL
SELECT 
  yr, subject, winner 
FROM 
  nobel 
WHERE 
  yr BETWEEN 1980 AND 1989 
  AND
  subject = 'Literature '
```

## 6. Only Presidents

```SQL
SELECT 
  * 
FROM
  nobel
WHERE 
  winner IN ('Theodore Roosevelt',
             'Woodrow Wilson',
             'Jimmy Carter',
             'Barack Obama')
```

## 7. John

```SQL
SELECT 
  winner
FROM
  nobel
WHERE
  winner LIKE 'John%'
```

## 8. Chemistry and Physics from different years

```SQL
SELECT 
  * 
FROM 
  nobel
WHERE
  (subject = 'Physics' AND yr = 1980)
  OR
  (subject = 'Chemistry' AND yr = 1984)
```

## 9. Exclude Chemists and Medics

```SQL
SELECT
  *
FROM
  nobel
WHERE
  subject NOT IN ('Chemistry', 'Medicine')
  AND
  yr = 1980
```

## 10. Early Medicine, Late Literature

```SQL
SELECT
  * 
FROM
  nobel 
WHERE
  (subject = 'Medicine' AND yr < 1910)
  OR
  (subject = 'Literature' AND yr >= 2004)
```

## 11. Umlaut

```SQL
SELECT 
  * 
FROM
  nobel 
WHERE
  winner LIKE 'PETER GRÜNBERG'
```

## 12. Apostrophe

```SQL
SELECT
  *
FROM
  nobel
WHERE
  winner = 'EUGENE O''NEILL'
```

## 13. Knights of the realm

```SQL
SELECT
  winner, yr, subject 
FROM
  nobel 
WHERE
  winner LIKE 'Sir%' 
ORDER BY
  yr DESC, winner
```

## 14. Chemistry and Physics last

```SQL
SELECT 
  winner, subject 
FROM 
  nobel 
WHERE 
  yr=1984
ORDER BY 
  CASE WHEN subject IN ('Chemistry','Physics') THEN 1 ELSE 0 END,
  subject, winner
``