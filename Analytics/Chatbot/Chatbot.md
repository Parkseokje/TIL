# Chatbot Analytics

Let's talk about how to group and visualize chatbot data.

## Environment

- Python: 3.7.3
- Jupyter lab [docs](https://jupyterlab.readthedocs.io/en/stable/getting_started/installation.html)
- OS: macOS Mojave

## Installing Python Modules

```python
import sys
!{sys.executable} -m pip install numpy pandas matplotlib
```

## Count by single group

```python
import pandas as pd

df = pd.read_csv('./data/chatlogs.csv')
df = pd.pivot_table(df, index=['intent'], values=['userId'], aggfunc=[len], fill_value=0)
print(df.head())
```

output:

```
intent      userId
alarm            2
application      5
array            9
bandwidth        5
bus              3
```

## Count by mutilpe groups

```python
import pandas as pd

df = pd.read_csv('./data/chatlogs.csv')
df = pd.pivot_table(df,index=['entityName','entityValue'],values=["userId"],aggfunc=[len],fill_value=0,margins=True)
print(df.head())
```

output:

```
entityName entityValue              userId
Bacon      Ergonomic Rubber Chips        1
           Fantastic Fresh Sausages      1
           Incredible Wooden Bacon       1
           Intelligent Frozen Mouse      1
           Rustic Steel Gloves           1
```

## Count by single group: date

User counts every hour

```python
import pandas as pd

df = pd.read_csv('../data/chatlogs.csv')
df['date']=pd.to_datetime(df['createdAt'],format='%Y%m%d %H:%M')
df.date = df.date.dt.tz_convert('Asia/Seoul') # (optional) Apply a different timezone

df.set_index('date').resample('1H')['userId'].count()
df.head()
```

output:

```
date
2020-02-10 20:00:00+09:00     48
2020-02-10 21:00:00+09:00    151
2020-02-10 22:00:00+09:00    132
2020-02-10 23:00:00+09:00    137
2020-02-11 00:00:00+09:00     89
```

To view the above data in a chart, simply do the follwing:

```python
import matplotlib.pyplot as plt

df1.plot()
plt.show()
```

## Get percentage of total with groupby

```python
import pandas as pd

df = pd.read_csv('../data/chatlogs.csv',sep=',')
df1 = df.groupby(['entityName','entityValue'])['userId'].agg(['count'])
df2 = (df1 / df1.groupby(level=0).sum() * 100).round(2)
df2.head()
```

output:

```
entityName	entityValue	              count
Bacon	      Ergonomic Rubber Chips	  20.0
            Fantastic Fresh Sausages	20.0
            Incredible Wooden Bacon	  20.0
            Intelligent Frozen  Mouse	20.0
            Rustic Steel Gloves	      20.0
```

## Find session id

Suppose that one session is 13 hours by the nature of the test data.

For simplicity, let's look at just one user.

- Convert datetime to timestamp
- Sort by timestamp ASC
- Calculate the different degrees of each timestamp.
- If the difference is more than 13 hours, it is assumed that it is a new session.
- If it is a new session, give a new session ID.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

df = pd.read_csv('../data/chatlogs.csv')
df['date']=pd.to_datetime(df['createdAt'],format='%Y%m%d %H:%M')
df.date = df.date.dt.tz_convert('Asia/Seoul')
df['timestamp'] = df.date.values.astype(np.int64) // 10 ** 9 # ts: timestamp

df1 = df[['userId', 'date', 'intent', 'timestamp']]

# Sort userId ASC, date DESC
df2 = df1.sort_values(['userId','timestamp'], ascending=[True,True])
df3 = df2[df2.userId == '9e4e1751-bbbd-414f-924e-0979cb580a36']

# Timestamp diff in seconds
diff_timestamp = df3.groupby('userId')['timestamp'].diff()

# indexes where new session_id will be created (for example here, The session interval is 13 hours.)
new_session = (diff_timestamp.isnull()) | (diff_timestamp > 60 * 60 * 13)

df3['session_id'] = df3.loc[new_session, ['userId', 'timestamp']] \
    .groupby('userId').rank(method='first').astype(int)

# Propagate last valid observation forward (replace NaN)
df3['session_id'] = df3['session_id'].fillna(method='ffill').astype(int)
df3.head()
```

output:

```
date	                            intent	  timestamp	  session_id
2020-01-02 08:04:29.273000+09:00	card	    1577919869	1
2020-01-07 10:17:19.484000+09:00	array	    1578359839	2
2020-01-07 22:36:27.781000+09:00	pixel	    1578404187	2
2020-01-12 14:12:11.031000+09:00	bandwidth	1578805931	3
2020-01-16 20:32:43.027000+09:00	card	    1579174363	4
```

## Pivot

- Display intents chronologically from left to right

```python
df3['rowNum'] = df3.groupby(['userId']).cumcount() + 1
pivot = df3.pivot_table(values=['intent'], index='userId', columns='rowNum', aggfunc='first')
pivot
```

output:

```
rowNum	  1	    2	    3	    4	        5	    6	   7
userId
9e4e1751	card	array	pixel	bandwidth	card	hard drive
```

## Sankey Diagrams

```python
# Sankey chart using plotly
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import plotly.graph_objects as go

df = pd.read_csv('../data/chatlogs_latest_21days.csv')
df['date']=pd.to_datetime(df['createdAt'],format='%Y%m%d %H:%M')
df.date = df.date.dt.tz_convert('Asia/Seoul')
df['timestamp'] = df.date.values.astype(np.int64) // 10 ** 9 # ts: timestamp

df1 = df[['userId', 'date', 'intent', 'timestamp']]

# Create unique indexes for each intent.
intents = pd.DataFrame(data=df1.intent.unique(), columns=['intent'])

# Find the last intent by user timeline
df2 = df1.sort_values(['userId','timestamp'], ascending=[True,True])
df2['prev_intent'] = df2.groupby('userId')['intent'].shift()

# Map the start and end points of each intent to the intent's index.
df3 = df2[df2.userId == '70fea51c-799b-4aa9-b649-f50cfe5e68ef']
df4 = df3.groupby(['prev_intent', 'intent'], as_index=False).size()
df5 = df4.reset_index(name='value')
df5['source'] = df5['prev_intent'].map(lambda x: intents[intents['intent'] == x].index[0])
df5['target'] = df5['intent'].map(lambda x: intents[intents['intent'] == x].index[0])

# Draw Sankey diagram
fig = go.Figure(data=[go.Sankey(
    node = dict(
      pad = 15,
      thickness = 20,
      line = dict(color = "black", width = 0.5),
      label = intents['intent'],
      color = "blue"
    ),
    link = dict(
      source = df5['source'],
      target = df5['target'],
      value = df5['value']
  ))])

fig.update_layout(title_text="Basic Sankey Diagram", font_size=10)
fig.show()
```

### Pitfalls

- The screen freezes when about 160,000 data are drawn in the sankey diagram.
- The final appearance of the diagram is reminiscent of the f1 arena, as you can return to the beginning or click `StartOver` button while using the chatbot.
- It must be expressed like chatbase's session flow to avoid nesting or circular reference structures.