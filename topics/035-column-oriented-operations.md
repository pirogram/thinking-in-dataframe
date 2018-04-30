code: column-oriented-operations
title: Column Oriented Operations
--- |

  As we discussed, `DataFrame` uses column oriented data layout. Each column's values are stored in one `ndarray`. In the parlance of data analysis, we can also say that all observations related to a single variable are stored in one `ndarray`. In this section, we'll look at some of the common computations we perform in data analysis. The objective is to reinforce that column oriented storage layout is indeed the right choice for a `DataFrame`.

  For the purpose of this discussion, let's look at a dataset related to [college majors](assets/data/fivethirtyeight--college-majors.csv). This data is sourced from [fivethirtyeight](https://github.com/fivethirtyeight/data/tree/master/college-majors). Feel free to download this dataset and play with it in your own Jupyter Notebook.

  This is what the dataset looks like:

  | Major_code|Major|Major_category|Total|Employed|Employed_full_time_year_round|Unemployed |
  | - | - | - | - | - | - | - |
  | 1100|GENERAL AGRICULTURE|Agriculture & Natural Resources|128148|90245|74078|2423 |
  | 1101|AGRICULTURE PRODUCTION AND MANAGEMENT|Agriculture & Natural Resources|95326|76865|64240|2266 |
  | 1102|AGRICULTURAL ECONOMICS|Agriculture & Natural Resources|33955|26321|22810|821 |
  | 1103|ANIMAL SCIENCES|Agriculture & Natural Resources|103549|81177|64937|3619 |
  | 1104|FOOD SCIENCE|Agriculture & Natural Resources|24280|17281|12722|894 |
  | 1105|PLANT SCIENCE AND AGRONOMY|Agriculture & Natural Resources|79409|63043|51077|2070 |
  | 1106|SOIL SCIENCE|Agriculture & Natural Resources|6586|4926|4042|264 |
  | 1199|MISCELLANEOUS AGRICULTURE|Agriculture & Natural Resources|8549|6392|5074|261 |
  | 1301|ENVIRONMENTAL SCIENCE|Biology & Life Science|106106|87602|65238|4736 |
  | 1302|FORESTRY|Agriculture & Natural Resources|69447|48228|39613|2144 |

---
type: live-code
id: 1
code: |
  import pandas as pd

  df = pd.read_csv('assets/data/fivethirtyeight--college-majors.csv')
  df.head()
--- |

  Please take a moment to [develop a perspective](/modules/a-perspective-on-data-in-data-analysis) about this dataset. This will aid in understanding rest of the material in this section.

  ## Summaries

  It's very common in data analysis to compute summaries of variables. To compute the summary, we take all values of one or more variables (aka column) and perform our computation.

  For example, let's take the `Major_category` variable in our dataframe. One way to summarize this data is:

  ```
  count             173
  unique             16
  top       Engineering
  freq               29
  Name: Major_category, dtype: object
  ```

  Here is the accompanying code in `Pandas` to generate this summary:

---
type: live-code
id: 2
code: |
  df['Major_category'].describe()
--- |

  We could also look at the number of majors in each of `Major_category`:

  ```
  Engineering                            29
  Education                              16
  Humanities & Liberal Arts              15
  Biology & Life Science                 14
  Business                               13
  Health                                 12
  Computers & Mathematics                11
  Agriculture & Natural Resources        10
  Physical Sciences                      10
  Psychology & Social Work                9
  Social Science                          9
  Arts                                    8
  Industrial Arts & Consumer Services     7
  Law & Public Policy                     5
  Communications & Journalism             4
  Interdisciplinary                       1
  ```

  Accompanying code for generating these proportions is:

---
type: live-code
id: 3
code: |
  df['Major_category'].value_counts()
--- |

  Yet another example is to find out the total percentage of full time employed professionals which happens to be `54.85%`. For this, we take a sum of `Employed_full_time_year_round` values and `Total` values and compute the percentage. And here is the code to perform this computation:

---
type: live-code
id: 4
code: |
  (100 * df['Employed_full_time_year_round'].sum()) / df['Total'].sum()
--- |

  ## Derived Variables

  Another common thing we do in data analysis is to derive new variables from existing variables. For example, we could create a new variable `Percentage_unemployment` that gives us an idea of percentage of people who remain unemployed for each major. For our dataset, it looks like the following:

  | Major | Percentage_unemployment	|
  | - | - |
  | GENERAL AGRICULTURE | 1.890783 |
  | AGRICULTURE PRODUCTION AND MANAGEMENT |   2.377106 |
  | AGRICULTURAL ECONOMICS |  2.417906 |
  | ANIMAL SCIENCES|  3.494964 |
  | FOOD SCIENCE  |   3.682043 |
  | PLANT SCIENCE AND AGRONOMY |  2.606757 |
  | SOIL SCIENCE  |   4.008503 |

  To compute this new variable, we took all values of `Unemployed` and `Total` variables and compute the percentages. Again, what we do here is take all values of select few columns and operate on those values. Here is the code for the same:

---
type: live-code
id: 5
code: |
  df['Percentage_unemployed'] = df['Unemployed'] * 100/df['Total']
  df[['Major', 'Percentage_unemployed']]
--- |

  ## Visualization

  Visualization, a key activity in data analysis, is again about exploring the relationship among variables or the distribution of values for a given variable.

  For example, the following graph shows the relative proportion of various values for `Major_category`.

  ![](assets/img/major-category-distribution.png)

  Here is another example that demonstrates the relationship between _major category_ and _average unemployment percentage_ within that category.

  ![](assets/img/percentage-unemployed.png)

  In both these instances, we again take select few variables and perform visualization across all values of those variables.

  Here is the code to generate both these plots:

---
type: live-code
id: 6
code: |
  import matplotlib.pyplot as plt

  # Relative proportions for major categories.
  df['Major_category'].value_counts().plot(kind='barh')

  # Relationship between major categories and average unemployment percentage.
  ( df[['Major_category', 'Percentage_unemployed']]
    .groupby('Major_category')
    .mean()
    .sort_values(by='Percentage_unemployed')
    .plot(kind='barh') )

  plt.show()
--- |

  ## Summary

  We just went through a handful of activities that we perform in data analysis. As we can see, the overall approach is to perform some computation on all values of select few columns. Column oriented storage layout provides significant efficiency in our computations.
