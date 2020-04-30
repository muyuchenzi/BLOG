文件目录
src-
    -myfuncitons_001.py
    -myfuncitons_002.py
main.py

1、myfuncitions之间进行函数引入是使用的是相对引用即：from .myfuncitions_001 import funciton01或者可以进行from src.myfuncitions_001 import myfuncition01
2、main.py中进行引入src中的函数是绝对引用from src.myfuncitions_002 import funciton02
3、这样所有的代码只有一个入口即：main 所以如果尽心写一些复杂的功能，需要进行详细规划，分配好各个模块的功能，这样才能进行优化
4、在pycharm中要注意自己运行的文件目录，run一下确定当前的入口，
