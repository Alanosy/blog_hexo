---
title: SSM
date: 2023-06-19 10:45
tags: [笔记]
---

## p1

## p2

## p3 初试 spring

## p4 系统架构

AOP 面向切面编程
Aspects AOP 思想实现
Core Container 核心容器
Data Access 数据访问
Data Integration 数据集成
web web 开发
test 单元测试与集成测试

## p5 核心概念

IoC/DI
IoC 容器
Bean

代码书写现状
耦合度偏高
解决方案
使用对象时，在程序中不要主动使用 new 产生对象，转换为由外部提供对象
IoC(Inversion of control)控制反转
对象的创建控制权由程序转移到外部，这种思想成为控制反转，也就是在完成降低耦合度
Spring 提供了一个容器成为 IoC 容器，用来从当 IoC 思想中的“外部”
IoC 容器复制对象的创建，初始化等一系列工作，被创建或被管理的对象在 IoC 容器中统称为 Bean

DI（Dependency Injection)依赖注入
在容器中简历 Bean 与 bean 之间的依赖关系的整个过程，成为依赖注入

目标:充分结耦
使用 IOC 容器管理 Bean(IOC)
在 Ioc 容器内将依赖关系的 bean 进行关系绑定（DI）
最终效果
使用对象时布局可以之间从 IOC 容器中获取，并且获取到的 bean 已经绑定了所有的依赖关系

## p6ioc 入门案例
