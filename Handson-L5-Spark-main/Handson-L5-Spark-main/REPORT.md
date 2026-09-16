# Hands-on L5: Report

**Name:Aidan Lopez**
**Student ID:801240291**
**Email:**

---

## What I ran

The commands you used, in the order you used them. If you deviated from the steps in the
README, say where and why.

```bash
docker compose up -d

docker compose -f docker-compose.codespaces.yml up -d

docker exec -it spark-master /opt/spark/bin/pyspark --master spark://spark-master:7077

from pyspark.sql.functions import explode, split, length, col
lines = spark.read.text("/opt/spark/work-dir/shared/input/data/input.txt")
words = lines.select(explode(split(col("value"), r"\s+")).alias("word"))
counts = words.filter(length("word") >= 3).groupBy("word").count()
counts.orderBy(col("count").desc(), col("word")).show()

docker cp wordcount.py spark-master:/opt/spark/work-dir/

docker exec -it spark-master /opt/spark/bin/spark-submit \
  --master spark://spark-master:7077 \
  /opt/spark/work-dir/wordcount.py \
  /opt/spark/work-dir/shared/input/data/input.txt \
  /opt/spark/work-dir/shared/output/wordcount


docker compose down
```

---

## Input and output

### My input dataset

```
The University of North Carolina at Charlotte (UNC Charlotte, or simply Charlotte) is a public research university in Charlotte, North Carolina, United States. UNC Charlotte offers 24 doctoral, 66 master's, and 79 bachelor's degree programs through nine colleges.[6] It is classified among "R1: Very High Research Spending and Doctorate Production."[7]

The university experienced rapid enrollment growth in the late 2000s and early-mid 2010s when it was the fastest-growing institution in the UNC System.[8]

It has two campuses: the Main Campus, located in University City, and the Center City Campus in Uptown Charlotte. The main campus sits on 1,000 wooded acres with approximately 85 buildings about 8 miles (13 km) from Uptown Charlotte.[9]

```

### The output of part 1

Paste the contents of the `part-...txt` file from `shared-folder/output/wordcount/`.

```
the 5
and 4
The 3
Charlotte 2
Charlotte, 2
North 2
UNC 2
University 2
Uptown 2
university 2
"R1: 1
(13 1
(UNC 1
1,000 1
2000s 1
2010s 1
Campus 1
Campus, 1
Carolina 1
Carolina, 1
Center 1
Charlotte) 1
Charlotte. 1
Charlotte.[9] 1
City 1
City, 1
Create 1
Doctorate 1
High 1
Main 1
Production."[7] 1
Research 1
Spending 1
States. 1
System.[8] 1
United 1
Very 1
about 1
acres 1
among 1
approximately 1
bachelor's 1
buildings 1
campus 1
campuses: 1
classified 1
colleges.[6] 1
dataset 1
degree 1
doctoral, 1
early-mid 1
enrollment 1
experienced 1
fastest-growing 1
from 1
growth 1
has 1
input 1
institution 1
km) 1
late 1
located 1
main 1
master's, 1
miles 1
nine 1
offers 1
own 1
programs 1
public 1
rapid 1
research 1
simply 1
sits 1
through 1
two 1
was 1
when 1
with 1
wooded 1
your 1


```

---

## What I observed

A few sentences on what you actually noticed. Some things worth looking at:

- What the master page at <http://localhost:8080> showed when the shell connected
- How many tasks and executors the Spark UI at <http://localhost:4040> listed for `show`
- How long the job took, in the shell and with `spark-submit`



---

## What I changed

The three changes you made to `wordcount.py`. Paste the lines you added or rewrote
(`git diff` gives you exactly this).

```python

```

---

## What the changes did

### The three numbers

| Run | Min length | Words scanned | Words kept | Distinct words |
| --- | ---------- | ------------- | ---------- | -------------- |
| `wordcount-v2` | 3 | | | |
| `wordcount-long` | | | | |

### The three outputs compared

How many distinct words did folding the case remove (compare `wordcount/` with
`wordcount-v2/`)? How many did the longer minimum remove? Name one word from your own text
whose count changed when the counting became case-insensitive.



### Jobs

How many jobs did your run launch, according to the **Jobs** tab, and how does that compare
with the original program? Why does Spark read the same file more than once in a single run?



---

## Problems and fixes

Anything that went wrong and what resolved it. Paste the actual error message. If nothing
went wrong, say so.


