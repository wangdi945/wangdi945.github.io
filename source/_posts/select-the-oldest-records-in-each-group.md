---
title: select the oldest records in each group
date: 2019-06-18 21:29:48
tags:
---
```sql
select
    group_id,
    min(concat(cast(add_time as char), "\t", cast(record_id as char)))
from
    record_table
group by
    group_id
```