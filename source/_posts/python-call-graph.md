---
title: python call graph
date: 2019-05-04 18:17:17
tags:
---
# 介绍
pycallgraph被设计成一个用于python应用程序的可视化分析工具。它使用一个名为sys.set_trace()的调试python函数，每次代码进入或离开函数时都会进行回调。这允许pycallgraph跟踪每个被调用函数的名称，以及调用哪个函数、每个函数内所用的时间、调用次数等。

# 安装
安装graphviz
```
sudo apt-get install graphviz

# test if graphviz works
dot -v
# output
dot - graphviz version 2.38.0 (20140413.2041)
There is no layout engine support for "dot"
Perhaps "dot -c" needs to be run (with installer's privileges) to register the plugins?

# follow the instruction
dot -c
```

安装pycallgraph
```
pip install pycallgraph
```

# 使用
```
# quick start
pycallgraph graphviz -- ./mypythonscript.py

# max depth
pycallgraph \
--max-depth=4 \
graphviz -- ./my_python_script.py

# exclude modules
pycallgraph \
--max-depth=4 \
-e "logging.*" \
graphviz -- ./my_python_script.py

pycallgraph \
--max-depth=4 \
-i "my_module.*" \
graphviz -- ./my_python_script.py
```

# 参考
http://pycallgraph.slowchop.com/en/master/index.html
