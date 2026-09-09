
## requests.utils.dict_from_cookiejar(cookiejar)

```python
requests.utils.dict_from_cookiejar(cookiejar)
```

👉 **把 `CookieJar` 对象，转换成普通的 Python 字典（dict）**

---

## 背景先搞清楚：CookieJar 是啥？

在 `requests` 里：

```python
response = requests.get(url)
response.cookies
```

你拿到的 **不是 dict**，而是一个：

```text
RequestsCookieJar
```

它长这样（逻辑上）：

```python
<RequestsCookieJar[<Cookie sessionid=abc123 for example.com/>]>
```

👉 这玩意 **不方便打印 / 断言 / 序列化**

---

## `dict_from_cookiejar()` 的作用

### 示例

```python
import requests
from requests.utils import dict_from_cookiejar

resp = requests.get("https://httpbin.org/cookies/set?token=abc")

cookies_jar = resp.cookies
cookies_dict = dict_from_cookiejar(cookies_jar)

print(cookies_dict)
print(type(cookies_dict))
```

输出：

```python
{'token': 'abc'}
<class 'dict'>
```

👉 **CookieJar → dict**

---

## 为什么不直接用 `response.cookies`？

因为：

|场景|CookieJar|dict|
|---|---|---|
|打印日志|❌ 不直观|✅ 清晰|
|pytest 断言|❌ 麻烦|✅ 简单|
|json.dumps|❌ 不支持|✅ 支持|
|参数传递|❌|✅|

---

## 自动化测试里的高频用法（重点）

### 1️⃣ 登录后断言 cookie

```python
cookies = dict_from_cookiejar(resp.cookies)

assert "sessionid" in cookies
assert cookies["sessionid"] != ""
```

---

### 2️⃣ 保存 cookie（比如写到文件 / redis）

```python
cookies_dict = dict_from_cookiejar(resp.cookies)

json.dumps(cookies_dict)
```

---

### 3️⃣ 多接口复用 cookie

```python
cookies = dict_from_cookiejar(login_resp.cookies)

requests.get(
    profile_url,
    cookies=cookies
)
```

👉 `requests` 的 `cookies=` **天然接收 dict**

---

## 和另一个函数是“成对”的

你会经常看到这一对 👇

```python
from requests.utils import dict_from_cookiejar, cookiejar_from_dict
```

### 反向操作

```python
jar = cookiejar_from_dict({"token": "abc"})
```

👉 **dict → CookieJar**

---

## 一个完整的“登录 → 访问资源”示例

```python
import requests
from requests.utils import dict_from_cookiejar

login_resp = requests.post(
    url="https://example.com/login",
    data={"user": "admin", "pwd": "123456"}
)

cookies = dict_from_cookiejar(login_resp.cookies)

profile_resp = requests.get(
    "https://example.com/profile",
    cookies=cookies
)
```

---

## 常见误区 ❌

### ❌ 以为 cookies 本身就是 dict

```python
json.dumps(response.cookies)  # TypeError
```

✔ 正确姿势：

```python
json.dumps(dict_from_cookiejar(response.cookies))
```

---

## 顺手给你一个更 Pythonic 的替代方案

### 用 `Session`（更推荐）

```python
session = requests.Session()

session.post(login_url, data=login_data)
resp = session.get(profile_url)
```

👉 **Session 自动维护 CookieJar**  
👉 根本不用你手动转 dict

但——  
**测试 / 断言 / 日志** 里，`dict_from_cookiejar()` 依然非常有用

---

## 一句话记忆法

> **CookieJar 是“给 requests 用的”  
> dict 是“给人和测试用的”**

---

如果你愿意，下一步我可以：

- 对比 **手动 cookie vs Session** 的优劣
    
- 或直接带你写一个 **pytest + requests + cookie 登录态测试**