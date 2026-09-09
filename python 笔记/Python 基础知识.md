`isinstance(obj, cls)`  
👉 **用来判断一个对象是不是某个类型（或其子类）的实例**

返回值只有两个：`True / False`

---

`json.dumps()`  
👉 **把 Python 对象，转换成 JSON 格式的字符串**

---

```python
**dict
```
👉 表示“把字典拆开成一组 key=value 形式的参数”

普通写法

```python
def login(username, password):
    print(username, password)

data = {
    "username": "admin",
    "password": "123456"
}

login(**data)
```

等价于：

```python
login(username="admin", password="123456")
```

👉 `**data` 就是 **“解包字典”**

```python
def func(a, b, **kwargs):
    print(a, b)
    print(kwargs)

func(1, 2, x=3, y=4)
```
输出：
```python
1 2
{'x': 3, 'y': 4}
```

```python
params = {
    "headers": {"Authorization": "token"},
    "timeout": 5
}

requests.get(url, **params)

```

