## SQL 基础
### MySQL如何避免重复插入数据？

### VARCHAR 后面代表字节还是字符？

### 说一下外键约束

### MySQL的关键字in和exist

### SQL查询语句的执行顺序是怎么样的？

![](attachments/Pasted%20image%2020260912154334.png)

### sql题
#### 给学生表、课程成绩表，求不存在01课程但存在02课程的学生的成绩

可以把它理解成 SQL 的逻辑执行过程：

```text
FROM
  ↓
JOIN
  ↓
得到一个中间结果集（你说的“虚拟表”）
  ↓
WHERE
  ↓
逐行过滤
  ↓
SELECT
  ↓
得到最终结果
```

对于你的 SQL：

```sql
SELECT s.sid, s.sname, sc2.cid, sc2.score
FROM Student s
LEFT JOIN Score AS sc1 
    ON s.sid = sc1.sid AND sc1.cid = '01'
LEFT JOIN Score AS sc2 
    ON s.sid = sc2.sid AND sc2.cid = '02'
WHERE sc1.cid IS NULL 
  AND sc2.cid IS NOT NULL;
```

可以先把 `FROM + JOIN` 想象成构造出这样的中间表：

| s.sid | s.sname | sc1.cid | sc1.score | sc2.cid | sc2.score |
| ----: | ------- | ------- | --------: | ------- | --------: |
|     1 | 张三      | 01      |        90 | 02      |        85 |
|     2 | 李四      | 01      |        80 | NULL    |      NULL |
|     3 | 王五      | NULL    |      NULL | 02      |        88 |
|     4 | 赵六      | NULL    |      NULL | NULL    |      NULL |

然后执行：
```sql
WHERE sc1.cid IS NULL AND sc2.cid IS NOT NULL
```

实际上就是**对这个中间结果集的每一行进行判断**。
例如：
```text
张三
sc1.cid = 01 → IS NULL？     ❌
```
不满足，过滤掉。
```text
李四
sc1.cid = 01 → IS NULL？     ❌
```
过滤掉。
```text
王五
sc1.cid = NULL → IS NULL？   ✅
sc2.cid = 02   → IS NOT NULL？✅
```
满足，保留。
所以最终：

| sid | sname | cid | score |
| --: | ----- | --- | ----: |
|   3 | 王五    | 02  |    88 |

---
不过有一个值得注意的地方：
你说：
> `FROM + JOIN` 先构造一个虚拟表，然后 `WHERE` 对每一行判断

这是**非常适合用来理解 SQL 的逻辑执行方式**的。

更严格地说，SQL 不是简单按照你写的从上到下逐条执行；这里说的是 **SQL 的逻辑执行顺序**。通常可以记成：

```text
FROM
  ↓
JOIN / ON
  ↓
WHERE
  ↓
GROUP BY
  ↓
HAVING
  ↓
SELECT
  ↓
ORDER BY
  ↓
LIMIT
```
所以你现在可以建立一个很重要的思维模型：
> **JOIN 负责“把哪些行组合起来”，WHERE 负责“这些组合出来的行哪些留下来”。**
这也是为什么 `ON` 和 `WHERE` 的位置有时候会影响 `LEFT JOIN` 的结果。

####   给定一个学生表 student_score（stu_id，subject_id，score），查询总分排名在5-10名的学生id及对应的总分

#### 如何用 MySQL 实现一个可重入的锁？