---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.1'
      jupytext_version: 1.2.4
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
---

# Arman Rafian


**Instructions:** This is an individual assignment, but you may discuss your code with your neighbors.


# Python and NumPy

While other IDEs exist for Python development and for data science related activities, one of the most popular environments is Jupyter Notebooks.

This lab is not intended to teach you everything you will use in this course. Instead, it is designed to give you exposure to some critical components from NumPy that we will rely upon routinely.

## Exercise 0
Please read and reference the following as your progress through this course. 

* [What is the Jupyter Notebook?](https://nbviewer.jupyter.org/github/jupyter/notebook/blob/master/docs/source/examples/Notebook/What%20is%20the%20Jupyter%20Notebook.ipynb#)
* [Notebook Tutorial](https://www.datacamp.com/community/tutorials/tutorial-jupyter-notebook)
* [Notebook Basics](https://nbviewer.jupyter.org/github/jupyter/notebook/blob/master/docs/source/examples/Notebook/Notebook%20Basics.ipynb)

**In the space provided below, what are three things that still remain unclear or need further explanation?**


Nothing so far


## Exercises 1-7
For the following exercises please read the Python appendix in the Marsland textbook and answer problems A.1-A.7 in the space provided below.


## Exercise 1

```python
import numpy as np
```

```python
a = np.full((6, 4), 2) # np.ones((6,4), dtype=int) * 2
display(a)
```

## Exercise 2

```python
b = np.ones((6,4))
np.fill_diagonal(b, 3)
display(b)
```

## Exercise 3

```python
a*b
```

```python
# np.dot(a, b) raises ValueError
```

a*b works because it is element-wise multiplication and they have the same dimensions

the dot product doesn't work because that does mattix multiplication which must have # rows of a same as # cols of b and # cols of a same as # rows of b


## Exercise 4

```python
np.dot(a.transpose(),b)
```

```python
np.dot(a, b.transpose())
```

They are different shape because of how matrix multiplication works. In the first case the number of cols of a transposed is 4 and the number of rows in b is 4 so it is a 4 by 4, and similar for a and b transpose.


## Exercise 5

```python
def func():
    print("Hello, World!")
```

```python
func()
```

## Exercise 6

```python
def randomStats():
    for i in range(5):
        randomArr = np.random.rand(1, 5)
        print('Stats for random array: {}'.format(randomArr))
        print('Sum: {}'.format(np.sum(randomArr)))
        print('Mean: {}'.format(np.mean(randomArr)))
        print('Median: {}'.format(np.median(randomArr)))
        print()
```

```python
randomStats()
```

## Exercise 7

```python
def numOnes(arr):
    c = 0
    for i in range(np.shape(arr)[0]):
        for j in range(np.shape(arr)[1]):
            if arr[i][j] == 1:
                c += 1
                
    return c
```

```python
print(numOnes(np.ones((2,2))))
print(numOnes(np.eye(2)))
print(numOnes(np.zeros((2,2))))
```

```python
len(np.where(np.ones((3,2)) == 1)[0])
```

## Excercises 8-???
While the Marsland book avoids using another popular package called Pandas, we will use it at times throughout this course. Please read and study [10 minutes to Pandas](https://pandas.pydata.org/pandas-docs/stable/getting_started/10min.html) before proceeding to any of the exercises below.


## Exercise 8
Repeat exercise A.1 from Marsland, but create a Pandas DataFrame instead of a NumPy array.

```python
import pandas as pd
```

```python
a = pd.DataFrame(np.full((6, 4), 2))
display(a)
```

## Exercise 9
Repeat exercise A.2 using a DataFrame instead.

```python
b = np.ones((6,4))
np.fill_diagonal(b, 3)
b = pd.DataFrame(b)
display(b)
```

## Exercise 10
Repeat exercise A.3 using DataFrames instead.

```python
a*b
```

```python
# pd.DataFrame.dot(a, b) raises ValueError as expected
```

The operations fail for the same reason as before since under the hood it is doing the same operation


## Exercise 11
Repeat exercise A.7 using a dataframe.

```python
def numOnes(df):
    c = 0
    for i in range(np.shape(df)[0]):
        for j in range(np.shape(df)[1]):
            if df.loc[i, j] == 1:
                c += 1
                
    return c
```

```python
display(numOnes(a))
numOnes(b)
```

```python
display(len(np.where(a == 1)[0]))
len(np.where(b == 1)[0])
```

## Exercises 12-14
Now let's look at a real dataset, and talk about ``.loc``. For this exercise, we will use the popular Titanic dataset from Kaggle. Here is some sample code to read it into a dataframe.

```python
titanic_df = pd.read_csv(
    "https://raw.githubusercontent.com/dlsun/data-science-book/master/data/titanic.csv"
)
titanic_df
```

Notice how we have nice headers and mixed datatypes? That is one of the reasons we might use Pandas. Please refresh your memory by looking at the 10 minutes to Pandas again, but then answer the following.


## Exercise 12
How do you select the ``name`` column without using .iloc?

```python
titanic_df['name']
```

## Exercise 13
After setting the index to ``sex``, how do you select all passengers that are ``female``? And how many female passengers are there?

```python
## YOUR SOLUTION HERE
titanic_df.set_index('sex',inplace=True)
titanic_df.loc['female']
```

```python
print("There were {} female passengers on the Titanic".format(titanic_df.loc['female'].shape[0]))
```

## Exercise 14
How do you reset the index?

```python
titanic = titanic_df.reset_index()
```

```python
titanic.head()
```
