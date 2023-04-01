---
title: Python虚拟环境
date: 2023/4/1 11:56:20 
tags: [技术分享]
---
### 一、使用virtualenv
1.使用pip
```
pip install virtualenv
```
2.创建运行环境
```
virtualenv [虚拟环境名称] 
virtualenv venv
 
#如果不想使用系统的包,加上–no-site-packeages参数
virtualenv  --no-site-packages 创建路径名
```
3. 激活环境
```
cd venv
source ./bin/activate
```
4. 退出环境
deactivate
5. 删除环境
没有使用virtualenvwrapper前，可以直接删除venv文件夹来删除环境
6. 使用环境
进入环境后，一切操作和正常使用python一样 安装包使用pip install 包
### 使用conda管理
1.创建虚拟环境
```
conda create -n vname python=3.9
```
2.激活虚拟环境
```
source activate vname
```
3.退出虚拟环境
```
source deactivate
```
4.删除虚拟环境
```
conda remove --vname venv --all
```
5.其他指令
```
# 列出系统存在虚拟环境
conda info -e
conda env list
 
# 查看当前环境下已安装的包
conda list
 
# 查看某个指定环境的已安装包
conda list -n venv
 
# 查找package信息
conda search numpy
 
# 安装package
conda install -n venv numpy
# 如果不用-n指定环境名称，则被安装在当前激活环境
# 也可以通过-c指定通过某个channel安装
 
# 更新package
conda update -n venv numpy
 
# 删除package
conda remove -n venv numpy
```
三、conda环境移植
第一步：激活需要迁移的虚拟环境
```
conda activate xxx
```
第二步：conda导出yml配置文件：
```
conda env export > xxx.yml
```
注：该配置文件内包四个字段：name / channels / dependencies（pip） / prefix，其中有两处需要修改

(1)name：U-2-Net
就是虚拟环境名称

(2)channels：
可以用来换源，默认为Default（这里我用的是清华源）
此处需要修改为：
```
channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/linux-64/
```
(3)dependencies：
一级是conda安装的包列表，子级pip下是pip安装的包列表，此处需要将pip以及下方该字段的相关列表删除。

此处需要修改（就把下面四行pip包相关直接删除掉）：
```
 - zstd=1.4.9=haebb681_0
  - pip:
    - analytics-python==1.3.1
    - appdirs==1.4.4
    - astor==0.8.1
```
(4)prefix: /home/changdunrui/anaconda3/envs/U-2-Net
虚拟环境路径(我的俩服务器路径一样，就没有修改，不一致时修改为目标anaconda的envs下就行)
第三步：pip导出库列表txt文件（一定要加–format）：
```
pip list --format=freeze > xxx.txt
```
第四步：将生成的两个文件(xxx.yml 和 xxx.txt)拷贝到新的服务器下面
第五步：在新服务器用如下命令创建新conda环境：
```
conda env create -f  xxx.yml
```
注：两个文件得在当前目录下，此时会将yml中conda库进行安装。自测pip包安装时间过长，所以在第二步删除pip字段，在第六步单独安装pip的包。

第六步：激活已创建的虚拟环境（同第一步）并安装pip的依赖包（这里pip我用的是豆瓣源）
```
conda activate xxx
pip install -r xxx.txt -i https://pypi.doubanio.com/simple/
```

