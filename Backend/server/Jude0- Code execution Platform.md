---
Created by: Shudipto Trafder
Created time: 2023-10-21T15:55
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:15
tags:
  - jude0
---
Get all languages

[http://localhost:2358/languages](http://localhost:2358/languages)

  

Submit a new issues

[http://localhost:2358/submissions](http://localhost:2358/submissions)

```Shell
source_code
language_id
```

full code

```Python
code = """import unittest

def add(a, b):
    return a + b
    
class TestAddFunction(unittest.TestCase):
    def test_add_positive_numbers(self):
        self.assertEqual(add(2, 3), 5)

    def test_add_negative_numbers(self):
        self.assertEqual(add(-2, -3), -6)

if __name__ == "__main__":
    unittest.main()
"""
    language_id = 71

    url = "http://localhost:2358/submissions/"

    res = requests.post(
        url,
        data={
            "source_code": code,
            "language_id": 71,
        }
    )
```

Get response about the program

[http://localhost:2358/submissions/0dd05119-4d0d-48bf-a34b-16f06a1ca1e5](http://localhost:2358/submissions/0dd05119-4d0d-48bf-a34b-16f06a1ca1e5)

```Python
token = res.json()['token']    
output = requests.get(url+token)
print(output.json())
```