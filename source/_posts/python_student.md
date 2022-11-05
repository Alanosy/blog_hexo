---
title: python列表实现学生成绩管理系统
date: 2022/11/5 23:33:23
tags: [Python]
---
## 引言
因为需要快速上手python，所以用python练了下学生成绩管理系统，现以实现初步增删改查功能，还有一些细节需要处理，源码如下：
```
list=[]
max = 100
def menu():
    print("===============")
    print("1、学生成绩录入")
    print("2、学生成绩删除")
    print("3、学生成绩修改")
    print("4、学生成绩查询")
    print("5、学生成绩打印")
    print("6、排       序")
    print("0、退       出")
    print("===============")
def add():
    for i in range(len(list),max):
        list.append([])
        print("请输入第", len(list), "位同学第学号", end=""), list[i].append(int(input()))
        print("请输入学号为", list[i][0], "的学生成绩", end=""), list[i].append(int(input()))
        b = str(input("还继续么（y/n）："))
        if b == 'y':
            pass
        elif b == 'n':
            break
        else:
            print("输入错误，即将退出")
            break

def dele():

    i=0
    a = int(input("请输入要删除信息的学号"))
    while (a!=list[i][0] and a<=len(list)):
        i += 1
    if a == list[i][0]:
        del list[i]
        print("删除成功")
    else:
        print("查无此人")
def alter():
    i = 0
    a = int(input("请输入要修改信息的学号"))
    while (a != list[i][0] and a <= len(list)):
        i += 1
    if a == list[i][0]:
        del list[i][1]
        print("请输入修改后的成绩：",end="")
        list[i].append(int(input()))
        print("修改成功")
    else:
        print("查无此人")
        print(len(list))
        print(a)
        print(i)
def find():
    i = 0
    a = int(input("请输入要修改信息的学号"))
    while (a != list[i][0] and a <= len(list)):
        i += 1
    if a == list[i][0]:
        print("查找到如下信息")
        print(list[i][0],list[i][1])
    else:
        print("查无此人")

def printfs():
    #print(list)
    for i in range(len(list)):
        print(list[i][0],list[i][1])


menu()
while(1):
    a = int(input("请输入需要使用的功能："))
    if a==1:
        add()
    elif a==2:
        dele()
    elif a==3:
        alter()
    elif a==4:
        find()
    elif a==5:
        printfs()
    elif a==0:
        break
    else:
        print("输入错误请重新输入")
```