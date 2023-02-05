# Using SQLite in Python
*[Ashkan Mirzaee](https://ashki23.github.io/index.html)*

[SQLite](https://www.sqlite.org/index.html) is a C-language library that
implements a small, fast, self-contained, high-reliability,
full-featured, SQL database engine. SQLite is the most used database
engine in the world.

  - [SQLite tutorial](https://www.sqlitetutorial.net/)
  - [SQLite Python](https://www.sqlitetutorial.net/sqlite-python/)
  - [Software
    Carpentry](http://swcarpentry.github.io/sql-novice-survey/)
  - [Database design with UML and
    SQL](http://web.csulb.edu/colleges/coe/cecs/dbdesign/dbdesign.php)

In this tutorial, we will learn how to convert CSV files to database
tables and run simple SQL queries in Python. We are using “surveys.csv”
and “species.csv” files from
[here](https://figshare.com/articles/dataset/Portal_Project_Teaching_Database/1314459/10)
to practice our learning.

-----

## Usage

SQLite can be used in GUI software such as [DB Browser for
SQLite](https://sqlitebrowser.org/). But there are a lot of advantages
to get queries directly in Python. In this document we are going to use
module `sqlite3` in Python to create a databases, import data and run
queries.

``` py
import sqlite3
```

To create a database (db) or connect to an existing one and to add a
cursor use:

``` py
con = sqlite3.connect('./mydb.db')
cur = con.cursor()
```

After setting “cur” pragma, we can start to execute SQL commands. For
instance to create a table, called “survey”, with some fields we can
run:

``` py
cur.execute("""
CREATE TABLE IF NOT EXISTS survey (
    record_id integer PRIMARY KEY,
    month text,
    day text,
    year text,
    plot_id text,
    species_id text,
    sex text,
    hindfoot_length real,
    weight real
    );""")
```

As you noticed we simply ran the SQL command to create the table with
`cur.execute`. Later we will use this method to run SQL queries.

## Importing data from CSV

Since we have a table, we can insert the data from “surveys.csv” into
“survey” table by:

``` py
with open('./surveys.csv', 'r') as fl:
    hd = fl.readline()[:-1].split(',')
    ro = fl.readlines()
    db = [tuple(ro[i][:-1].split(',')) for i in range(len(ro))]

cur.executemany("INSERT INTO survey (record_id,month,day,year,plot_id,species_id,sex,hindfoot_length,weight) VALUES (?,?,?,?,?,?,?,?,?);", db)
```

We need to commit the changes and close the connection to store the data
into “survey” table:

``` py
con.commit()
con.close()
```

The following function can be used to insert CSV data to a database
table. It adds fields’ name based on the CSV header and types from
inputs:

``` py
#!/usr/bin/python3

import sqlite3

def csv_sql(file_dir,table_name,database_name,fields_type):
    con = sqlite3.connect(database_name)
    cur = con.cursor()
    # Drop the current table before re-create:
    cur.execute("DROP TABLE IF EXISTS %s;" % table_name)

    with open(file_dir, 'r') as fl:
        hd = fl.readline()[:-1].split(',')
        ro = fl.readlines()
        db = [tuple(ro[i][:-1].split(',')) for i in range(len(ro))]

    zip_ = list(zip(hd,list(fields_type)))
    hd_fl = ['%s %s' % (x,y) for x,y in zip_]
    header_field = ','.join(hd_fl)
    header = ','.join(hd)
    cur.execute("CREATE TABLE IF NOT EXISTS %s (%s);" % (table_name,header_field))
    cur.executemany("INSERT INTO %s (%s) VALUES (%s);" % (table_name,header,('?,'*len(hd))[:-1]), db)
    con.commit()
    con.close()
    
if __name__ == '__main__':
    # Example
    fields_type_1 = ['integer PRIMARY KEY'] + ['text']*6 + ['real']*2
    fields_type_2 = ['text PRIMARY KEY'] + ['text']*3
    csv_sql('./surveys.csv','survey','eco.db',fields_type_1)
    csv_sql('./species.csv','species','eco.db',fields_type_2)
```

## Queries

Let’s use the above function to convert “survey.csv” and “species.csv”
to tables in “eco.db”. Now, we can use `execute` command for running SQL
commands in Python. For example:

``` python
import sqlite3

# Connect and read the db
con = sqlite3.connect('./eco.db')
cur = con.cursor()

# SQL query
cur.execute("SELECT DISTINCT year FROM survey;") # select unique survey years

# Store output
out = cur.fetchall()
print(out)

## [('1977',), ('1978',), ('1979',), ('1980',), ('1981',), ('1982',), ('1983',), ('1984',), ('1985',), ('1986',), ('1987',), ('1988',), ('1989',), ('1990',), ('1991',), ('1992',), ('1993',), ('1994',), ('1995',), ('1996',), ('1997',), ('1998',), ('1999',), ('2000',), ('2001',), ('2002',)]

# Close the connection
con.close()

# Output as a list
lis = [x[0] for x in out]
print(lis)

## ['1977', '1978', '1979', '1980', '1981', '1982', '1983', '1984', '1985', '1986', '1987', '1988', '1989', '1990', '1991', '1992', '1993', '1994', '1995', '1996', '1997', '1998', '1999', '2000', '2001', '2002']
```

In the above example we stored the output as a Python list. We can also
store the queries in Python dictionaries:

``` python
import sqlite3

# Connect and read the db
con = sqlite3.connect('./eco.db')
cur = con.cursor()

# SQL query
cur.execute("SELECT name FROM PRAGMA_TABLE_INFO('survey');") # select fields' name

# Store output
out = cur.fetchall()
name = [x[0] for x in out]
print(name)

## ['record_id', 'month', 'day', 'year', 'plot_id', 'species_id', 'sex', 'hindfoot_length', 'weight']

# Exe query, store output and close the connection
cur.execute('SELECT * FROM survey LIMIT 2;') # select first two rows
out = cur.fetchall()
con.close()
print(out)

## [(1, '7', '16', '1977', '2', 'NL', 'M', 32.0, ''), (2, '7', '16', '1977', '3', 'NL', 'M', 33.0, '')]

# Output as a list of dictionaries
d = []
for i in out:
    d.append(dict(zip(name,i)))
print(d)

## [{'record_id': 1, 'month': '7', 'day': '16', 'year': '1977', 'plot_id': '2', 'species_id': 'NL', 'sex': 'M', 'hindfoot_length': 32.0, 'weight': ''}, {'record_id': 2, 'month': '7', 'day': '16', 'year': '1977', 'plot_id': '3', 'species_id': 'NL', 'sex': 'M', 'hindfoot_length': 33.0, 'weight': ''}]
```

The following are more examples of different SQL queries in Python:

``` python
import sqlite3

# Connect and read the db
con = sqlite3.connect('./eco.db')
cur = con.cursor()

# Queries
cur.execute("SELECT ROUND(weight/1000,2) FROM survey LIMIT 2;") # change weight to kg
print(cur.fetchall())
## [(0.0,), (0.0,)]

cur.execute("""
SELECT ROUND(weight/1000,2) 
FROM survey 
WHERE (year > 2000) AND (species_id IN ('DM','DS','DO')) AND (weight > 1)
LIMIT 2;""")
print(cur.fetchall())
## [(0.04,), (0.05,)]

cur.execute("""
SELECT species_id, sex, count(*) FROM survey
WHERE species_id IN ('DS','DO')
GROUP BY sex, species_id
ORDER BY count(*) DESC;""")
print(cur.fetchall())
## [('DO', 'M', 1707), ('DO', 'F', 1308), ('DS', 'M', 1270), ('DS', 'F', 1188), ('DS', '', 46), ('DO', '', 12)]

cur.execute("""
SELECT species_id, sex, count(*) FROM survey
GROUP BY sex, species_id
HAVING species_id IN ('DS','DO')
ORDER BY count(*) DESC;""")
print(cur.fetchall())
## [('DO', 'M', 1707), ('DO', 'F', 1308), ('DS', 'M', 1270), ('DS', 'F', 1188), ('DS', '', 46), ('DO', '', 12)]

cur.execute("""
SELECT species_id, sex, count(*) FROM survey
WHERE species_id LIKE 'D%'
GROUP BY sex, species_id
ORDER BY count(*) DESC;""")
print(cur.fetchall())
## [('DM', 'M', 5969), ('DM', 'F', 4554), ('DO', 'M', 1707), ('DO', 'F', 1308), ('DS', 'M', 1270), ('DS', 'F', 1188), ('DM', '', 73), ('DS', '', 46), ('DX', '', 40), ('DO', '', 12)]

cur.execute("""
SELECT * FROM survey
JOIN species
ON species.species_id = survey.species_id
WHERE weight < 5 AND sex = 'F'
LIMIT 2;""")
print(cur.fetchall())
## [(4052, '4', '5', '1981', '3', 'PF', 'F', 15.0, 4.0, 'PF', 'Perognathus', 'flavus', 'Rodent'), (5346, '2', '22', '1982', '21', 'PF', 'F', 14.0, 4.0, 'PF', 'Perognathus', 'flavus', 'Rodent')]

cur.execute("""
SELECT species_id ||'-'|| species FROM species;""")
print(cur.fetchone())
## ('AB-bilineata',)
```

Note that:

  - We can use `fetchall()` to fetch all outputs and `fetchone()` to get
    the first query
  - In `LIKE` operator, the wildcard `%` matches zero or more
    characters, so that `%able%` matches `fixable` and `tablets`
  - And we can combine fields by `||'<separator>'||`

Also, we can use SQLite3 directly from command line for getting queries.
For example, change the directory to your database location and enter
`sqlite3 eco.db` to open the database and run:

``` sql
.schema -- to see the schema of the databse
.tables -- to list database tables
.mode column -- to see in column mode
.header on -- to show headers
PRAGMA TABLE_INFO(species); -- to see tables info
SELECT * FROM survey ORDER BY year ASC LIMIT 10;
```

---

Copyright 2018-2023, [Ashkan Mirzaee](https://ashki23.github.io/index.html) | Content is available under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | Sourcecode licensed under [GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)
