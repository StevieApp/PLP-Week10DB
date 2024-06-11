<!--
 Copyright 2024 Steve Nginyo
 
 Licensed under the Apache License, Version 2.0 (the "License");
 you may not use this file except in compliance with the License.
 You may obtain a copy of the License at
 
     https://www.apache.org/licenses/LICENSE-2.0
 
 Unless required by applicable law or agreed to in writing, software
 distributed under the License is distributed on an "AS IS" BASIS,
 WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 See the License for the specific language governing permissions and
 limitations under the License.
-->

# Week 9

I noted that some fields were accepted as empty and arrays (directors, casts, country) and Movies and TV shows were supported

# Week 10

Seems same as week 10
Was able to reexport the data in an sql file

# week 11

Only 100 records were being imported used the following code to import all 8807 records

```
    USE 8week;
    SHOW VARIABLES LIKE "secure_file_priv";
    LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.4/Uploads/netflix_titles.csv' INTO TABLE netflix_titles
    fields terminated by ','
    enclosed by '"'
    lines terminated by '\n'
    ignore 1 lines;
```

# week 12

```
SELECT *
FROM 
    `8week`.`netflix_titles`
WHERE 
    `title` LIKE '%night%'
ORDER BY 
    `description`;
```

Only 85 records had a variation of the word 'night'


# week 13
```
SELECT 
    `release_year`,
    COUNT(*) AS `number_of_titles`,
    GROUP_CONCAT(`title` SEPARATOR '; ') AS `titles`,
    MAX(`rating`) AS `highest_rating`
FROM 
    `8week`.`netflix_titles`
WHERE 
    `description` LIKE '%the%'
GROUP BY 
    `release_year`;
```
Only 72 rows fit this criteria

# week 14
```
SELECT 
    `release_year`,
    COUNT(*) AS `number_of_titles`,
    GROUP_CONCAT(`title` SEPARATOR '; ') AS `titles`,
    MAX(`rating`) AS `highest_rating`,
    ROUND(AVG(`rating`)) AS `average_rating`,
    CASE
        WHEN YEAR(CURDATE()) - `release_year` > 10 THEN 'old'
        WHEN YEAR(CURDATE()) - `release_year` < 2 THEN 'new'
        ELSE 'recent'
    END AS `aging`
FROM 
    `8week`.`netflix_titles`
WHERE 
    `description` LIKE '%time%'
GROUP BY 
    `release_year`;
```
Only 35 fit this criteria of including 'time' and only 8 were recent and none were new, the rest were old

# week 15
```
SELECT 
    `release_year`,
    COUNT(*) AS `number_of_titles`,
    GROUP_CONCAT(`title` SEPARATOR '; ') AS `titles`,
    MAX(`rating`) AS `highest_rating`,
    CONCAT('the "', `title`, '" was released in ', `release_year`, ' and was added on ', `date_added`) AS formatted_string
FROM 
    `8week`.`netflix_titles`
WHERE 
    `description` LIKE '%the%' AND
    `cast` LIKE '%Tracy%'
GROUP BY 
    `release_year`;
```
11 rows fit this criteria where the cast has 'Tracy' with a new string speaking about the movie

# Week 16
```
SELECT 
    `release_year`,
    COUNT(*) AS `number_of_titles`,
    GROUP_CONCAT(DISTINCT `title` SEPARATOR '; ') AS `titles`,
    MAX(`rating`) AS `highest_rating`,
    GROUP_CONCAT(DISTINCT CONCAT('the "', `title`, '" was released in ', `release_year`, ' and was added on ', `date_added`) SEPARATOR '; ') AS formatted_strings,
    GROUP_CONCAT(DISTINCT CASE
        WHEN `cast` LIKE '%Greta%' THEN `cast`
        ELSE NULL
    END SEPARATOR ', ') AS `cast_including_greta`
FROM 
    `8week`.`netflix_titles`
WHERE 
    `description` LIKE '%Lisa%'
GROUP BY 
    `release_year`
HAVING 
    `cast_including_greta` IS NOT NULL;
```
1 row fit thid criteria where cast has 'Greta' and description includes 'Lisa'


# GRAPHS INCLUDED WITH CSV USED