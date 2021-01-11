# big-data-apache-spark-python

## Getting Started with Spark

### Installing Python, a JDK, Spark and its Dependencies

https://sundog-education.com/spark-python/

https://medium.com/luckspark/installing-spark-2-3-0-on-macos-high-sierra-276a127b8b85

#### 

MacOS

#### Step 1: Install Apache Spark

```
brew install apache-spark
```

(substitute 3.0.1 for the version actually installed)
```
cd /usr/local/Cellar/apache-spark/3.0.1/libexec/conf
```

```
cp log4j.properties.template log4j.properties
```

Edit the log4j.properties file and change the log level from INFO to ERROR on log4j.rootCategory.

from 
```
log4j.rootCategory=INFO, console
```
to
```
log4j.rootCategory=ERROR, console
```

#### Step 2: Install Anaconda

Install the latest Anaconda for Python 3 from anaconda.com

https://www.anaconda.com/products/individual#macos

#### Step 3: Test it out!

- Open up a terminal
- cd into the directory where you installed Spark, and then ls to get a directory listing.
- Look for a text file we can play with, like README.md or CHANGES.txt
- Enter `pyspark`
- At this point you should have a >>> prompt. If not, double check the steps above.
- Enter `rdd = sc.textFile("README.md")` (or whatever text file you’ve found) Enter `rdd.count()`
- You should get a count of the number of lines in that file! Congratulations, you just ran your first Spark program!
- Enter quit() to exit the spark shell, and close the terminal window
- You’ve got everything set up! Hooray!

### Getting the MovieLens Movie Rating Dataset

- https://grouplens.org/datasets/movielens/
- http://files.grouplens.org/datasets/movielens/ml-100k.zip

### Ratings histogram example

```python
from pyspark import SparkConf, SparkContext
import collections

conf = SparkConf().setMaster("local").setAppName("RatingsHistogram")
sc = SparkContext(conf = conf)

lines = sc.textFile("ml-100k/u.data")
ratings = lines.map(lambda x: x.split()[2])
result = ratings.countByValue()

sortedResults = collections.OrderedDict(sorted(result.items()))
for key, value in sortedResults.items():
    print("%s %i" % (key, value))
```

```
cd ~/Documents/SparkCourse
```

```
spark-submit ratings-counter.py
```

You should see an output like this:
```
1 6110
2 11370
3 27145
4 34174
5 21201
```

### What's new in Spark 3?

Deprecation:
- MLLib is deprecated (sort of) - the one that's based on the RDD interface
- Python 2 support is deprecated

Benefits:
- Spark 3 is faster, even 17 times faster than Spark 2
- GPU instance support
- Deeper Kubernetes Support
- Binary File Support
- SparkGraph - Cypher Query Language
- ACID support in data lakes with Delta Lake - https://delta.io/





