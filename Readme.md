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
