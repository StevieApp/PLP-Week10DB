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