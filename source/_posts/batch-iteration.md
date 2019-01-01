---
title: python 分批迭代 list
date: 2019-01-01 19:46:31
tags:
---

在用 python 处理大量数据时，经常需要将数据拆成若干批次，分批进行处理。例如：将 10 万条数据插入数据库，比较好的方式是分批插入，每次插入 1000 条。

```python
BATCH_SIZE = 3

some_list = range(10)
total_num = len(some_list)

for start in range(0, total_num, BATCH_SIZE):
    batch = some_list[start : start + BATCH_SIZE]
    # do something with this batch
    print batch
```