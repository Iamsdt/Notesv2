---
Created by: Shudipto Trafder
tags:
  - jwt
  - backend
Last edited time: 2025-02-02T22:59:00
---
## **JWT Algorithm Performance and Security Comparison**

### **Benchmark Results (100x Encoding & Decoding)**

| Algorithm   | Type       | Time (s)   | Security                                            | Use Case                                    |
| ----------- | ---------- | ---------- | --------------------------------------------------- | ------------------------------------------- |
| **HMAC**    | Symmetric  | **0.0009** | 🔓 Less secure (shared secret)                      | Ultra-fast authentication, internal systems |
| **HS256**   | Symmetric  | **0.0041** | 🔓 Less secure (shared secret)                      | Internal APIs, trusted parties              |
| **RS256**   | Asymmetric | 0.5586     | 🔒 Strong (public-private key)                      | Public APIs, third-party clients            |
| **PS256**   | Asymmetric | 3.6992     | 🔒 Stronger than RS256 (padding for extra security) | High-security needs                         |
| **Ed25519** | Asymmetric | 0.0279     | 🔒 Stronger than RS256, smaller keys                | Modern, efficient security                  |
| **ES256**   | Asymmetric | 0.0358     | 🔒 Secure, but complex                              | Mobile, IoT, high-security apps             |

---

### **Performance Comparison**

Below is a graph showing the relative encoding/decoding times of each algorithm:

```plaintext
HMAC    | █
HS256   | ████
RS256   | ████████████████
PS256   | ██████████████████████████████████████████
Ed25519 | ██████
ES256   | ███████
```

This visual clearly shows that **HMAC is the fastest**, followed by **HS256**, while **PS256 is the slowest**.

---

### **Choosing the Right Algorithm**

| **Use Case**                         | **Recommended Algorithm** | **Reason**                                             |
| ------------------------------------ | ------------------------- | ------------------------------------------------------ |
| Ultra-fast authentication (internal) | **HMAC**                  | Fastest, but shared secret risk                        |
| Internal APIs, speed-critical apps   | **HS256**                 | Fast, but shared secret risk                           |
| Public APIs, third-party clients     | **RS256**                 | Strong security with public-private key rotation       |
| High-security applications           | **PS256**                 | Stronger than RS256, better protection against attacks |
| Modern, efficient security           | **Ed25519**               | Faster than RSA, stronger security                     |
| Mobile, IoT, high-security apps      | **ES256**                 | Secure, optimized for compact keys                     |

### **Best Balance?**

🚀 **Use `Ed25519` or `ES256`** if you want both speed & strong security.


Code
```python
import datetime

import hashlib

import hmac

import time

  

import jwt

  
  

# HS256 implementation

def hs256_jwt():

shared_secret = "mysecret"

payload = {"data": "test"}

token = jwt.encode(payload, shared_secret, algorithm="HS256")

decoded = jwt.decode(token, shared_secret, algorithms=["HS256"])

return decoded

  
  

# RS256 implementation

def rs256_jwt():

# Sample RSA keys for demonstration purposes

private_key = """-----BEGIN RSA PRIVATE KEY-----

MIICWgIBAAKBgGUfD5S73T7S5PY9deQ7Oa3ojd1KXIwZ0l4qgU5JdIAg8P2Y54DF

O2fJKV1lh8G8MveUcdegz5B0/NbMryvZIaDqt5KlHq3tbkHhj4HlRTnwGPDWM8Y4

HXz4sAcNhT7PTv9he2HFR3DUv62XWef68kwQ8yRrWlEI8MnpK6ly3nFFAgMBAAEC

gYBAn8AaYpE7ZBYVVCPyjvMGtFdtc+d/VcU+jtWCTalZdTPuLfjNL78OTd3UpV1E

L902ojS7BDeCb3FiaP8N+77kRRQiEUfq/axFAKx+fXv4GtDTw/yjCcgpW044JGCa

mq/bQorgmtjL7GA6H1EuLC71hqbBbOL9whl2YMiq77fS5QJBAKkp8OdT65yqsjQ+

dCF3Gdg73PmB/Je1zNHNzbVPTVqudvpX3x3A8RkJG38hEb/yNTHZsMyc/VRmKhQd

+xrVIxMCQQCZB47xkbF6i7coD2Hxb8EnGIQMOJM7ITNa297hIIOBoZQOeS3RXhR3

0sUGWRBWab3a1mMslZfjEqTOXciyl01HAkB14MgCKrRwQ3JSfYKnHztfNrfRFgdS

IFlNib/irBQXMKOv5zOOpDhdXb9PY1ffDYSL7EoLCwpsmZSQ2CN2mzcJAkByMZK4

r3jaMrJdoYT8DuH7E69OE1XC9RaGgbaDFqkrrfB3EHRhXSw28kB2aTXo1gWH7R2a

opLyLvJu0Ms4gfF3AkBe9UycUtsUSrbkXc9E9B5HJRSw5SIyCdz+mjy2AJpIHhUx

k/JFE3IuwUZCjarmR3lPONx+UgL+ACqJ6RWzwRSk

-----END RSA PRIVATE KEY-----"""

public_key = """-----BEGIN PUBLIC KEY-----

MIGeMA0GCSqGSIb3DQEBAQUAA4GMADCBiAKBgGUfD5S73T7S5PY9deQ7Oa3ojd1K

XIwZ0l4qgU5JdIAg8P2Y54DFO2fJKV1lh8G8MveUcdegz5B0/NbMryvZIaDqt5Kl

Hq3tbkHhj4HlRTnwGPDWM8Y4HXz4sAcNhT7PTv9he2HFR3DUv62XWef68kwQ8yRr

WlEI8MnpK6ly3nFFAgMBAAE=

-----END PUBLIC KEY-----"""

payload = {"data": "test"}

token = jwt.encode(payload, private_key.encode("utf-8"), algorithm="RS256")

decoded = jwt.decode(token, public_key.encode("utf-8"), algorithms=["RS256"])

return decoded

  
  

def ps256():

private_key = "-----BEGIN RSA PRIVATE KEY-----\nMIIEogIBAAKCAQEAuNhCS6bodtd+PvKqNj+tYZYqTNMDkf0rcptgHhecSsMP9Vay\n+6NvJk1tC+IajPaE4yRJVY4jFqEt3A0MJ9sKe5mWDYFmzW/L6VzQvQ+0nrMc1YTE\nDpOf7BQhlW5W0mDj5SwSR50Lxg/acb+SMWq6zmhuAoLRapH17K2RWONA2vr2frox\nJ6N9TGtrQHygDb0p9D6jPnXEe4y+zBuj6o0bCkJgCVNM+CU19xBepj5caetYV28/\n49yl5XPi93n1ATU+7aGAKxuvjudODuHhF/UsZScMFSHeZW367eQldTB2w9uoIIzW\nO46tKimr21zYifMimjwnBQ/PLDqc7HqY0Y/rLQIDAQABAoIBAAdu0CD7/Iu61/LE\nDfV8fgZXOYA5WVgSLCBsVbh1Y+2FsStBFJVrLwRanLCbo6GuJWMqNGC3ryWGebJI\nPAg7lfepEhBHodClAY1yvq9mOvHJa2Fn+KegEWWMMbAxQwCBW5NS6waXhBUE0i3n\ncYOB3TKA9IYuqH52kW22VQqT/imlWEb28pJJT49YfggmOOtAkrKerokO53lAfrJA\ntm8lYvxXnfnuYh7zI835RpZJ1PeaYrMqyAwT+StD9hPKGWGpN1gCJijjcK0aapvq\nMLET/JxMxxcLsINOeLtGhMKawmET3J/esJTumOE2L77MFG83rlCPbsSfLdSAI2WD\nSe3Q2ikCgYEA7JzmVrPh7G/oILLzIfk8GHFACRTtlE5SDEpFq+ARMprfcBXpkl+Q\naWqQ3vuSH7oiAQKlvo3We6XXohCMMDU2DyMaXiQMk73R83fMwbFnFcqFhbzx2zpm\nj/neHIViEi/N69SHPxl+vnUTfeVZptibNGS+ch3Ubawt3wCaWr+IdAcCgYEAx/19\ns5ryq2oTQCD5GfIqW73LAUly5RqENLvKHZ2z+mZ0pp7dc5449aDsHPLXLl1YC3mO\nlZZk+8Jh5yrpHyljiIYwh/1y0WsbungMlH6lG9JigcN8R2Tk9hWT7DQL0fm0dYoQ\njkwr/gJv6PW0piLsR0vsQQpm/F/ucZolVPQIoisCgYA5XXzWznvax/LeYqRhuzxf\nrK1axlEnYKmxwxwLJKLmwvejBB0B2Nt5Q1XmSdXOjWELH6oxfc/fYIDcEOj8ExqN\nJvSQmGrYMvBA9+2TlEAq31Pp7boxbYJKK8k23vu87wwcvgUgPj0lTdsw7bcDpYZT\neI1Xu3WyNUlVxJ6nm8IoZwKBgG6YPjVekKg+htrF4Tt58fa95E+X4JPVsBrBZqou\nFeN5WTTzUZ+odfNPxILVwC2BrTjbRgBvJPUcr6t4zWZQKxzKqHfrrt0kkDb0QHC2\nAHR8ScFc65NHtl5n3F+ZAJhjsGn3qeQnN4TGsEBx8C6XzXY4BDSLnhweqOvlxJNQ\nSJ31AoGAX/UN5xR6PlCgPw5HWfGd7+4sArkjA36DAXvrAgW/6/mxZZzoGA1swYdZ\nq2uGp38UEKkxKTrhR4J6eR5DsLAfl/KQBbNC42vqZwe9YrS4hNQFR14GwlyJhdLx\nKQD/JzHwNQN5+o+hy0lJavTw9NwAAb1ZzTgvq6fPwEG0b9hn0SI=\n-----END RSA PRIVATE KEY-----\n"

public_key = "-----BEGIN PUBLIC KEY-----\nMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAuNhCS6bodtd+PvKqNj+t\nYZYqTNMDkf0rcptgHhecSsMP9Vay+6NvJk1tC+IajPaE4yRJVY4jFqEt3A0MJ9sK\ne5mWDYFmzW/L6VzQvQ+0nrMc1YTEDpOf7BQhlW5W0mDj5SwSR50Lxg/acb+SMWq6\nzmhuAoLRapH17K2RWONA2vr2froxJ6N9TGtrQHygDb0p9D6jPnXEe4y+zBuj6o0b\nCkJgCVNM+CU19xBepj5caetYV28/49yl5XPi93n1ATU+7aGAKxuvjudODuHhF/Us\nZScMFSHeZW367eQldTB2w9uoIIzWO46tKimr21zYifMimjwnBQ/PLDqc7HqY0Y/r\nLQIDAQAB\n-----END PUBLIC KEY-----\n"

encoded = jwt.encode({"some": "payload"}, private_key, algorithm="PS256")

res = jwt.decode(encoded, public_key, algorithms=["PS256"])

return res

  
  

def edds():

private_key = "-----BEGIN PRIVATE KEY-----\nMC4CAQAwBQYDK2VwBCIEIPtUxyxlhjOWetjIYmc98dmB2GxpeaMPP64qBhZmG13r\n-----END PRIVATE KEY-----\n"

public_key = "-----BEGIN PUBLIC KEY-----\nMCowBQYDK2VwAyEA7p4c1IU6aA65FWn6YZ+Bya5dRbfd4P6d4a6H0u9+gCg=\n-----END PUBLIC KEY-----\n"

encoded = jwt.encode({"some": "payload"}, private_key, algorithm="EdDSA")

res = jwt.decode(encoded, public_key, algorithms=["EdDSA"])

return res

  
  

def es256():

private_key = b"-----BEGIN EC PRIVATE KEY-----\nMHcCAQEEIHAhM7P6HG3LgkDvgvfDeaMA6uELj+jEKWsSeOpS/SfYoAoGCCqGSM49\nAwEHoUQDQgAEXHVxB7s5SR7I9cWwry/JkECIRekaCwG3uOLCYbw5gVzn4dRmwMyY\nUJFcQWuFSfECRK+uQOOXD0YSEucBq0p5tA==\n-----END EC PRIVATE KEY-----\n"

public_key = b"-----BEGIN PUBLIC KEY-----\nMFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAEXHVxB7s5SR7I9cWwry/JkECIReka\nCwG3uOLCYbw5gVzn4dRmwMyYUJFcQWuFSfECRK+uQOOXD0YSEucBq0p5tA==\n-----END PUBLIC KEY-----\n"

encoded = jwt.encode({"some": "payload"}, private_key, algorithm="ES256")

jwt.decode(encoded, public_key, algorithms=["ES256"])

  
  

def hmac_test():

key = "secret key"

expiry = (datetime.datetime.now() + datetime.timedelta(minutes=15)).isoformat()

message = f"6820698575169822721:admin:{expiry}"

signature = hmac.new(key.encode(), message.encode(), hashlib.sha256).hexdigest()

# now generate signature again

# to make it fare, same as above

message = f"6820698575169822721:admin:{expiry}"

signature = hmac.new(key.encode(), message.encode(), hashlib.sha256).hexdigest()

  
  

if __name__ == "__main__":

# Measure time for HS256 function repeated 100 times

start_hs = time.time()

for _ in range(100):

hs256_jwt()

end_hs = time.time()

print("HS256 loop time:", end_hs - start_hs)

  

# Measure time for RS256 function repeated 100 times

start_rs = time.time()

for _ in range(100):

rs256_jwt()

end_rs = time.time()

print("RS256 loop time:", end_rs - start_rs)

  

# Measure time for RS256 function repeated 100 times

start_rs = time.time()

for _ in range(100):

ps256()

end_rs = time.time()

print("PS256 loop time:", end_rs - start_rs)

  

# Measure time for RS256 function repeated 100 times

start_rs = time.time()

for _ in range(100):

edds()

end_rs = time.time()

print("Ed25519 loop time:", end_rs - start_rs)

  

# Measure time for RS256 function repeated 100 times

start_rs = time.time()

for _ in range(100):

es256()

end_rs = time.time()

print("ES256 loop time:", end_rs - start_rs)

  

# Measure time for HMAC function repeated 100 times

start_hmac = time.time()

for _ in range(100):

hmac_test()

end_hmac = time.time()

print("HMAC loop time:", end_hmac - start_hmac)

  
  

### RESULT ###

# HS256 loop time: 0.004616737365722656

# RS256 loop time: 0.585801362991333

# PS256 loop time: 3.7913498878479004

# Ed25519 loop time: 0.030477523803710938

# ES256 loop time: 0.044251203536987305
```