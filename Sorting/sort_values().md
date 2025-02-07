The sort_values() function in pandas is used to sort a DataFrame by one or more columns. It's a versatile and powerful function that allows for sorting in various ways, including ascending or descending order, and it can handle complex sorting scenarios based on multiple columns.

**Syntax**

DataFrame.sort_values(by, axis=0, ascending=True, inplace=False, kind='quicksort', na_position='last', ignore_index=False, key=None)

**Parameters**

- **by**: The column label or list of labels to sort by. This parameter is required.
- **axis**: {0 or ‘index’, 1 or ‘columns’}, default 0. It specifies whether to sort rows (0) or columns (1).
- **ascending**: Bool or list of bools, default True. If True, sorts in ascending order; if False or a list of bools, sorts in descending order.
- **inplace**: Bool, default False. If True, performs the operation in place and returns None. By default, it returns a new DataFrame.
- **kind**: Specifies the sorting algorithm; options include ‘quicksort’, ‘mergesort’, ‘heapsort’, etc. The default is ‘quicksort’.
- **na_position**: {‘first’, ‘last’}, default ‘last’. It determines whether NaN values are put at the beginning or end of the sorted DataFrame.
- **ignore_index**: Bool, default False. If True, the resulting index will be labeled 0, 1, …, n - 1.
- **key**: Function that takes a Series as input and returns a Series. This parameter allows for custom sorting based on complex criteria.

**Detailed Examples**

**Initial Setup**

Let’s create a sample DataFrame for these examples:

import pandas as pd

data = {

'Name': \['Alice', 'Bob', 'Charlie', 'David', 'Eve', 'Frank', 'Grace'\],

'Age': \[24, 30, 22, 29, 35, 28, 24\],

'Salary': \[50000, 60000, 45000, 52000, 80000, 75000, 58000\],

'Department': \['HR', 'IT', 'Finance', 'HR', 'IT', 'Finance', 'IT'\]

}

df = pd.DataFrame(data)

print(df)

**Output of the DataFrame**

Name Age Salary Department

0 Alice 24 50000 HR

1 Bob 30 60000 IT

2 Charlie 22 45000 Finance

3 David 29 52000 HR

4 Eve 35 80000 IT

5 Frank 28 75000 Finance

6 Grace 24 58000 IT

**Example 1: Basic Sorting**

To sort the DataFrame by Age in ascending order:

sorted_df = df.sort_values(by='Age')

print(sorted_df)

**Output**

Name Age Salary Department

2 Charlie 22 45000 Finance

0 Alice 24 50000 HR

6 Grace 24 58000 IT

3 David 29 52000 HR

1 Bob 30 60000 IT

5 Frank 28 75000 Finance

4 Eve 35 80000 IT

**Example 2: Sorting in Descending Order**

You can sort by Salary in descending order:

sorted_df_desc = df.sort_values(by='Salary', ascending=False)

print(sorted_df_desc)

**Output**

Name Age Salary Department

4 Eve 35 80000 IT

5 Frank 28 75000 Finance

1 Bob 30 60000 IT

0 Alice 24 50000 HR

3 David 29 52000 HR

2 Charlie 22 45000 Finance

6 Grace 24 58000 IT

**Example 3: Sorting by Multiple Columns**

You can sort by multiple columns. For instance, sort by Department first and then by Salary within each department:

sorted_multi = df.sort_values(by=\['Department', 'Salary'\], ascending=\[True, False\])

print(sorted_multi)

**Output**

Name Age Salary Department

2 Charlie 22 45000 Finance

5 Frank 28 75000 Finance

0 Alice 24 50000 HR

3 David 29 52000 HR

1 Bob 30 60000 IT

4 Eve 35 80000 IT

6 Grace 24 58000 IT

**Example 4: Handling NaN Values**

You can specify the position of NaN values when sorting:

\# Introducing NaN values

df_with_nan = df.copy()

df_with_nan.loc\[3, 'Salary'\] = None # Setting David's salary to NaN

\# Default: NaN values will be at the end

sorted_nan_default = df_with_nan.sort_values(by='Salary')

print(sorted_nan_default)

**Output**

Name Age Salary Department

2 Charlie 22 45000 Finance

0 Alice 24 50000 HR

5 Frank 28 75000 Finance

1 Bob 30 60000 IT

4 Eve 35 80000 IT

3 David 29 NaN HR

**Example: To Place NaN at the Start**

sorted_nan_first = df_with_nan.sort_values(by='Salary', na_position='first')

print(sorted_nan_first)

**Output**

Name Age Salary Department

3 David 29 NaN HR

2 Charlie 22 45000 Finance

0 Alice 24 50000 HR

5 Frank 28 75000 Finance

1 Bob 30 60000 IT

4 Eve 35 80000 IT

**Example 5: Sorting with Custom Sort Key**

If you need to apply a custom sorting function, you can use the key parameter. For example, sorting by the length of the names:

sorted_by_length = df.sort_values(by='Name', key=lambda x: x.str.len())

print(sorted_by_length)

**Output**

Name Age Salary Department

0 Alice 24 50000 HR

1 Bob 30 60000 IT

2 Charlie 22 45000 Finance

3 David 29 52000 HR

4 Eve 35 80000 IT

5 Frank 28 75000 Finance

6 Grace 24 58000 IT

**Example 6: In-Place Sorting**

If you want to sort the DataFrame in place without creating a new object, you can use the inplace parameter:

df.sort_values(by='Age', inplace=True)

print(df)

**Output**

This will sort the original DataFrame by Age:

Name Age Salary Department

2 Charlie 22 45000 Finance

0 Alice 24 50000 HR

6 Grace 24 58000 IT

3 David 29 52000 HR

1 Bob 30 60000 IT

5 Frank 28 75000 Finance

4 Eve 35 80000 IT

**Summary**

The sort_values() function in pandas is a powerful tool for organizing your DataFrame based on one or more columns. By using parameters such as by, ascending, inplace, and key, you can customize the sorting behavior to fit your analysis needs. This function is essential in data cleaning and preprocessing tasks, enabling more effective data exploration and visualization.
