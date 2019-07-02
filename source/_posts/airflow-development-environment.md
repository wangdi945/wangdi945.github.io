---
title: airflow development environment
date: 2019-07-02 21:20:25
tags:
---
# 前言
本文主要介绍Mac下如何安装Airflow开发环境。

# 安装python3
## 安装XCode
```
xcode-select --install
```

## 安装Homebrew
```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
# 设置环境变量
export PATH=/usr/local/bin:/usr/local/sbin:$PATH
```

## 安装python3
```
brew install python3
```

### 报错：Permission denied @ dir_s_mkdir - /usr/local/Frameworks
```
sudo mkdir /usr/local/Frameworks
sudo chown $(whoami):admin /usr/local/Frameworks
```

# 安装Airflow开发环境
## 下载源码
```
git clone https://github.com/apache/airflow.git
```

## 安装airflow
参考INSTALL和run_unit_tests.sh
```
# 方法一
pip install -e .
# 方法二
python setup.py develop
```

## 安装开发依赖
```
pip install 'apache-airflow[devel]'
```

## 安装mysqlclient
### 安装mysql开发包
```
brew install mysql-connector-c
```

### 修改mysql_config
增加写权限
```
chmod 755 /usr/local/bin/mysql_config
vi /usr/local/bin/mysql_config
```
change
```
# on macOS, on or about line 112:
# Create options
libs="-L$pkglibdir"
libs="$libs -l "
```
to
```
# Create options
libs="-L$pkglibdir"
libs="$libs -lmysqlclient -lssl -lcrypto"
```

# unittest
参考run_unit_tests.sh
```bash
# environment
export AIRFLOW_HOME=~/airflow
export AIRFLOW__CORE__UNIT_TEST_MODE=True

# add test/contrib to PYTHONPATH
DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" && pwd )"
export PYTHONPATH=$PYTHONPATH:${DIR}/tests/test_utils

# Generate the `airflow` executable if needed
which airflow > /dev/null || python setup.py develop

# Initialize the DB
echo "Initializing the DB"
yes | airflow initdb
yes | airflow resetdb

# To run individual tests:
nosetests tests.jobs.test_scheduler_job:SchedulerJobTest.test_is_alive
```