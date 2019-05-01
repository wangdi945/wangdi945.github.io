---
title: airflow quick start
date: 2019-05-01 19:49:09
tags:
---
# 前言
airflow是一个以编程的方式编写、调度和监控工作流的平台，并支持与第三方平台的集成。

- 2014年，诞生于Airbnb
- 2016年，进入Apache孵化器
- 2019年，1月8日毕业成为Apache顶级项目

# 安装
安装选用的是airflow最新的版本，1.10.3。
```
pip install apache-airflow==1.10.3
```

安装过程中如果有依赖包的版本较新，无法通过pip源安装，可以通过github安装。
```
# install requests==2.21.0
pip install git+https://github.com/requests/requests.git@v2.21.0
# install flask-admin==1.5.3
pip install git+https://github.com/flask-admin/flask-admin.git@v1.5.3
```

# 运行
配置airflow文件夹
```
export AIRFLOW_HOME=~/airflow
```

初始化数据库
```
airflow initdb
```

启动webserver和scheduler
```
nohup airflow webserver -p 8080 > ${AIRFLOW_HOME}/logs/server.log 2>&1 &
nohup airflow scheduler > ${AIRFLOW_HOME}/logs/scheduler.log 2>&1 &
```

停止
```
$(ps -ef | grep airflow | grep -v grep | awk '{print "kill -9 "$2}')
```

# 参考
- [airflow官方文档](http://airflow.apache.org/start.html)
- [pip支持从git上安装包](https://pip.pypa.io/en/stable/reference/pip_install/#vcs-support)