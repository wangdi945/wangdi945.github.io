---
title: linux生成连续时间戳
date: 2018-10-11 21:04:23
tags:
---

```bash
#!/bin/bash

set -u  # 使用的变量必须提前定义过
set -e  # 所有非 0 的返回状态都需要捕获
set -o pipefail  # 管道间错误需要捕获

#help info
if [[ "$#" -ne "2" ]];then
    echo "Usage: date_creater.sh start_date end_date"
    echo "Examples: date_creater.sh 2000-01-01 2000-01-02"
    exit 1
fi

start_date="$1"
end_date="$2"

# 自定义函数
function my_func() {
    local cur_date="$1"
    echo "${cur_date}"
}

start_sec=$(date -d ${start_date} +%s)
end_sec=$(date -d ${end_date} +%s)
interval_days=$(( (end_sec - start_sec) / 86400 )) # 一天有 86400 秒

for((i=0; i<=interval_days; i++)); do
    date_string="${start_date} +${i} days"
    cur_date="$(date -d "${date_string}" +%F)"
    my_func ${cur_date}
done
```