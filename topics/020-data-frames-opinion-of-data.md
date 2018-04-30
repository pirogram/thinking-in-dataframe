code: data-frames-opinion-of-data
title: DataFrame's Opinion of Data
--- |

  The RDBMS' opinion of data is that it is a tabular structure. Each column has a name, a data type and potentially other constraints (e.g. uniqueness, reference to another column in another table, value range etc). RDBMS also has an important concept of Primary Key which results in unique identifiers for each row in the table.

  At a high level, a DataFrame's opinion of the data is very similar. Data is arranged in a table. Each column has a name (also called label) and a data type. `DataFrame` does not have the concept of a Primary Key since it does not try to uniquely identify each row. Instead, it has the concept of _Index_ which is used for labeling the rows. As we look into examples later on, the function of Index (or row labels) will become clear.

  Let's look at a small sample dataset to get an understanding of how pandas looks at data. We'll load a dataset that looks like the following:

  | city          | max_temp | min_temp |
  |---------------|----------|----------|
  | San Francisco | 105      | 25       |
  | San Diego     | 125      | 40       |
  | Los Angeles   | 115      | 35       |
  | Santa Barbara | 112      | 33       |
  | San Jose      | 110      | 30       |

  The following code loads a sample dataset [temperature.csv](assets/data/temperature.csv) using the `read_csv` function in Pandas.

---
type: live-code
id: 1
code: |
  import pandas as pd

  df = pd.read_csv('assets/data/temperature.csv')
  df.head()
--- |

  You can also download the [temperature.csv](assets/data/temperature.csv) file and load it in your own Jupyter Notebook. Here is an annotated version of the DataFrame that we just created:

  ![]('assets/img/dataframe-anatomy.png')

  As expected, the `DataFrame` has 3 columns (`city`, `max_temp`, `min_temp`) and 5 rows. The unusual or unexpected thing that we see here is `Index`. As we discussed earlier, `DataFrame` has the concept of _Index_ which is used for labeling the rows. We'll see the usefulness of labeling the rows later. For now, suffice it to say that `Pandas` auto generated the labels for rows since we didn't provide any from labels (aka Index) our side.

---
type: multiple-choice-question
id: 2
question: "Select the statements that are true:"
options:
  - text: A `DataFrame` always has an `Index` even if it's not provided by us.
    correct: true
  - text: Each row in the `DataFrame` must have a unique label.
    help: This is not true. Multiple rows in a `DataFrame` can have the same label.
  - text: Default `Index` of a `DataFrame` is a monotonically increasing number that starts from 0.
    correct: true
