# Python vs Spark
*[Ashkan Mirzaee](https://ashki23.github.io/index.html)*

There are many tools to handle structured and smi-structured data. Two
of the most popular tools are Python and Spark. Python’s packages like
Pandas are famous for ease of use and applying conventional dataframes,
while Spark uses a more SQL type datafame on top of a Java engine and is
well known for big data analysis. Spark has an interface for Python that
is called PySpark. To compare Python and Spark, here we use Pyspark.

-----

## Syntax

Let’s first look at some syntax from each of Python and PySpark. The
following shows some basic tasks using Pandas:

``` py
import pandas as pd

# Read a CSV file
df = pd.read_csv('./file.csv')
df
#   brand  rank
# 0  Ford     1
# 1   GMC     2
# 2   AMC     3

# Ford's rank (we know that right! ;))
df['rank'][df['brand'] == 'Ford']
# 1

# Get a list of ranks
df['rank'].tolist()
# [1, 2, 3]

# Number of rows that has Ford's name (without specifying the column's name)
sum(df.isin(['Ford']).any(axis = 1))
# 1

# Add a new column from a list 
df['note'] = ['1st', '2nd', '3rd']
df
#   brand  rank  note
# 0  Ford     1   1st
# 1   GMC     2   2nd
# 2   AMC     3   3rd
```

The following are very similar tasks using PySpark:

``` py
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName('test_spark').getOrCreate()

# Read a CSV file
df = spark.read.csv('./file.csv', header = True)
df.show()
# +-----+----+
# |brand|rank|
# +-----+----+
# | Ford|   1|
# |  GMC|   2|
# |  AMC|   3|
# +-----+----+

# Ford's rank (again! :))
df.filter(df['brand'] == 'Ford').show()
# +-----+----+
# |brand|rank|
# +-----+----+
# | Ford|   1|
# +-----+----+

# Get a list of ranks
[int(x[0]) for x in df.select('rank').collect()]
# [1, 2, 3]

# Number of rows that has Ford's name (I have to passed the column's name!)
df.filter(df['brand'] == 'Ford').count()
# 1

# Add a new column from a list 
# Amost not doable without a unique key!
```

In general, PySpark is not as user friendly as Pandas and it sometimes
can be hard to write some simple tasks.

## When using Spark

Despite the harder syntax, Spark has a great advantage that shines when
the data is big (\> 1 TB)\! Spark distributed processes by assigning a
main controller node and several worker nodes (each note can be one or
more cores) to split the tasks. That means Spark will parallelize the
computational tasks out of the box. For example, if you want to count a
string in a large database, Spark can split the data among the worker
nodes. Each worker does the counting on a chunk of data and returns the
result to the controller node. Eventually the controller node aggregates
the results and tells us the total. So, if you have “big data” to
analyze, then Spark could be a better tool than Python.

Note that Spark is designed to work with large data and therefore it
relies on both hard drives and RAMs (in many cases store the data on
hard drives to prevent RAMs’ overflow). Using hard drives makes the
read/write process much slower and can increase the time and this is the
sacrifice that we need to make when the data is large\!

## When using Python

Python (and many of its packages like Pandas) does not distribute the
processes in multiple cores and instead uses a single core - no matter
how many free cores are available. Note that it does not mean that we
cannot run parallel jobs in Python. We can always use some packages or
create our own job submission method to run multiple parallel tasks at
the same time. But in general we can say that Python can be very fast as
long as the data can fit into the RAM and a single core can handle the
process. With the new advances in CPUs and RAMs technologies, this type
of processing has become more and more popular. So, if we have numerous
tiny tasks, Python and its native packages can be a very helpful option
to use. For instance, when you have a small dataset (\< 1 GB) but you
want to run 100s of independent analysis on that data, Python can be a
better solution than Spark.

## A real use case: do an hour job in a couple of minutes\!

In one of my projects, we are looking to forecast next month’s shipment
for several commodity groups. We have a data that shows actual shipments
of each commodity group in addition to the supplier promises for several
months. We are using many heuristic methods and several regression
analysis to find the best forecast with the least error. We developed
this project for both Spark and Python and found interesting results
when comparing these two\! To run the workflows, we use a GCP instance
with 64 cores and 160GB RAMs.

First, we developed our workflow in PySpark with using Spark ML library
for our regression analysis. We submit a single job for each commodity
group to find the best forecast and start all jobs in parallel. For
instance, when we have 20 commodity groups, we submit 20 jobs together
with assigning 3 cores to each (using 60 cores out of 64 cores). Since
each job has 3 cores, Spark uses 2 workers (with one core each) and
keeps one core for the controller node. Even though our tasks are not
CPU intensive, we found that in reality there were not enough resources
for Spark to distribute the process and reduce the computational time
practically. Note that by using Spark we are assigning one third of are
resources just for the controller nodes for some simple processes. By
using PySpark we were able to finish the computational tasks for all
commodity groups in about an hour.

After trying Spark, we decided to use Python to see if we can expedite
the process. We developed a new workflow using Pandas and Scikit-learn
instead of Spark. When we used the same job submission method, we
realized that each job can be done much faster in Python (on one core
only\!). With Python we did not also need to assign several cores for
the controller nodes, that let us to run more jobs at each time. By
using Python we were able to finish the computational tasks for all
commodity groups in a couple of minutes\!

---

Copyright 2018-2021, [Ashkan Mirzaee](https://ashki23.github.io/index.html) | Content is available under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | Sourcecode licensed under [GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)
