---
tags:
  - ai
  - pandas
Date: 2024-05-07T22:00:00
---

#### Reshaping by pivoting

*Unpivots* a DataFrame from wide format to long (stacked) format,
```python
staked = pd.melt(users, id_vars="name", var_name="variable", value_name="value")
print(staked)
```

“pivots” a DataFrame from long (stacked) format to wide format,
```python
print(staked.pivot(index='name', columns='variable', values='value'))
```
