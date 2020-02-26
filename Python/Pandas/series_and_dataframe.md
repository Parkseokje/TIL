# Series and Dataframe

## Series

- A Series is a one-dimensinal object
- It can hold any data type
- Series consists of index label and value
- Value can be accessed via index label
- Index can be duplicated

### Simple series

```python
import pandas as pd

x = pd.Series([1,2,3])
x

index   values
--------------
0       1
1       2
2       3

x[0]
1
```

## Define new index

```python
x = pd.Series([1,2,3], index=['a','b','c'])
x

index   values
--------------
a       1
b       2
c       3

x['a']
1
```

## Dictionary type series

```python
data = {'abc': 1, 'def': 2, 'xyz': 3}
x = pd.Series(data)
x

index   values
--------------
abc     1
def     2
xyz     3

x['abc']
1
```

## Scalar value series

The value gets repeated for each of the indexed defined.

```python
x = pd.Series(1, index=['a','b','c'])
x

index   values
--------------
a       1
b       1
c       1
```

## Dataframe

- A Dataframe is a two dimensinal object that can have columns
- Dictionaries, lists, series can be included
- Most commonly used pandas object

## Dataframe with Numpy

```python
import numpy as np
import pandas as pd

dates = pd.date_range('20200226', periods=3)
# DatetimeIndex(['2020-02-26', '2020-02-27', '2020-02-28'], dtype='datetime64[ns]', freq='D')
columns = list('ABC')
['A', 'B', 'C']

data = np.random.randn(3,3)
# array([[-0.10914734, -0.75659384, -0.06899813],
#        [ 1.37714538,  2.09279708, -0.05586049],
#        [ 0.2282605 , -1.54231927, -0.34941844]])

df = pd.DataFrame(data, index=dates, columns=columns)
df


index       A	        B	        C
--------------------------------------------
2020-02-26	0.109953	-0.134801	0.023890
2020-02-27	1.417591	0.800834	0.145955
2020-02-28	-1.428734	0.438276	0.422585
```

## Get Summary of our data

```python
df.describe()

	     A	         B	        C
-----------------------------------------
count	 3.000000	 3.000000	3.000000
 mean	-0.297529	-0.695912	0.751660
  std	 0.966246	 1.045112	0.839380
  min	-1.155043	-1.624613	-0.167104
  25%	-0.820992	-1.261776	0.388307
  50%	-0.486941	-0.898940	0.943717
  75%	 0.131229	-0.231561	1.211043
  max	 0.749398	 0.435818	1.478368
```

## Get cumulative sum

```python
df.apply(np.cumsum)


            A	         B	         C 
---------------------------------------------
2020-02-26	-0.076596	-0.470757	 0.109522
2020-02-27	 1.390033	-0.875267	-1.120344
2020-02-28	 1.504389	-0.522906	-3.327057
```

## Referenced site

 - [Series and DataFrame in Python](https://www.freecodecamp.org/news/series-and-dataframe-in-python-a800b098f68/)
