
# Vyshnavi Daka:

Notebook: https://colab.research.google.com/drive/1qlPjDdo3P9AzbX_D2LJVvyVnG1py4tn-?authuser=1#scrollTo=7LekGPFSMnGw

5. Top 10 users with high daily app usage
Code
```python
power_users = (
    usage
    | "Map UserID and AppUsageTime" >> beam.Map(app_map_class)
    | "Get Top 10 Users" >> beam.combiners.Top.Of(10, key=lambda users: users[1])
    | "Flatten Top 10 List" >> beam.FlatMap(lambda users: users)
    | "Print All Users" >> beam.Map(lambda user: print(user) or user)
    | "Extract User IDs Only" >> beam.Map(lambda userid: userid[0])
    | "Write Power Users" >> beam.io.WriteToText('power_users.txt')
)

```

Why Flatten?
Lets understand: beam.combiners.Top.Of(10, key=lambda users: users[1]) transform finds the top 10 users based on the specified key (in this case, `users[1]`, which is app usage time). However, `Top.Of` returns the result as a **single-element list containing the top 10 entries**.
Here:

- We have **one list with 10 tuples** inside it.
- This list itself is a single item in the PCollection.
```python
data = [(i, v) for i, v in enumerate(range(20))]
data | beam.combiners.Top.Of(10, key=lambda users: users[1])
```

Output:
```python
[[(19, 19),
  (18, 18),
  (17, 17),
  (16, 16),
  (15, 15),
  (14, 14),
  (13, 13),
  (12, 12),
  (11, 11),
  (10, 10)]]
```

Now flatten:
```python
output | beam.FlatMap(lambda users: users)
```
Output:
```python
[(19, 19),
 (18, 18),
 (17, 17),
 (16, 16),
 (15, 15),
 (14, 14),
 (13, 13),
 (12, 12),
 (11, 11),
 (10, 10)]
```

