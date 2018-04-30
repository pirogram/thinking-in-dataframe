code: column-oriented-storage
title: Column Oriented Storage
--- |

  Let's consider a simple dataset in the tabular format:

  | name               | handle         | date       | text |
  |--- |--- |--- |
  | Computer Science   | CompSciFact    | 2018-01-17 | Generating primes in Conway's Game of Life http://www.nathanieljohnston.com/2009/08/generating-sequences-of-primes-in-conways-game-of-life/ |
  | I Am Developer     | iamdeveloper   | 2018-01-17 | my favourite thing about standing desks, they keep me on my toes |
  | Srinath Srininvasa | srinaths       | 2018-01-17 | Deep learning is so yesterday, let's talk deep happiness :) |

  There are two ways to lay out this data in memory. One approach is called row-oriented. You take all the values from a row, pack them together and place them in memory. Take all values of next row, pack them together and place them next to the data from first row. So on so forth. Second approach is called column-oriented. Take all values from one column, pack them together and place them in memory. Take all values from next column, pack them together and place them next to first column's values. So on so forth.

  There is also a hybrid approach where we take a bunch of rows and pack them in column oriented layout. The take next bunch of rows and pack them in column oriented layout. So on so forth. Since, this is much harder to implement, most systems stick to either row oriented or column oriented approach.

  RDBMS (e.g. MySQL, PostgreSQL etc) use the the row oriented approach to layout the data. This is because the applications that use RDBMS often perform CRUD operations on a single record (or a limited few records). The main concerns in RDBMS world would be:

  * How to add a new tweet?
  * How to read a tweet by given id or last 10 tweets by a user?
  * How to delete a tweet?

  Row oriented approach to layout data is optimized for these kind of operations that operate on one or select few records at a time.

  On the other hand, systems like Pandas use column oriented approach to layout the data. This is because during data analysis, we work at _variable_ level. We would usually operate on all the values of one or more variables in one shot. Whether we plot one variable against another (e.g. max_temp vs city) or calculate statistical summaries (e.g. average max_temp) or change the metric (Fahrenheit to Celsius), we operate at the column level. Most importantly, a dataset may have hundreds of variables and we might work with just a handful of them at a time. Column oriented approach to data layout makes it easy to select all values of select few variables while ignoring the rest. All this is true for analytical systems in general.

  Let's look at some concrete examples of this column oriented approach to data layout. Here we load the sample [temperature.csv](assets/data/temperature.csv) dataset:

---
type: live-code
id: 1
code: |
  import pandas as pd

  df = pd.read_csv('assets/data/temperature.csv')
  df
--- |

  We can now look at the data type of various columns:

---
type: live-code
id: 2
code: |
  df['max_temp']
--- |

  As you can see, `max_temp` is stored as a datatype `int64`. Pandas `DataFrame` columns are actually backed by `ndarray`. So, in this dataframe (`df`), all values of `city` column are stored in one `ndarray`, all values of `max_temp` in another `ndarray` and ditto for `min_temp`. Here is the code to look at the underlying `ndarray`.

---
type: live-code
id: 3
code: |
  # access ndarray for min_temp column
  df['min_temp'].values

---
type: live-code
id: 4
code: |
  # access ndarray for max_temp column
  df['max_temp'].values

---
type: live-code
id: 5
code: |
  # access ndarray for city column
  df['city'].values

---
type: multiple-choice-question
id: 6
question: |
  Download the sample [tweets.csv](assets/data/tweets.csv) dataset and load it as a `DataFrame` in a Jupyter Notebook. Based on your inspection of the `DataFrame`, select the true statements from the following:
options:
  - text: |
      `name` variable has the data type `object`.
    correct: true
  - text: |
      `name` variable has the data type `string`.
  - text: |
      `date` variable has the data type `object`.
    correct: true
  - text: |
      `date` variable has the data type `date`.
    help: Pandas has the ability to parse the dates but we need to pass relevant options to `read_csv` method.
