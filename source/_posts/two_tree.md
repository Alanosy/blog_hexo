---
title: 学生成绩管理系统——二叉树
date: 2022/12/9 10:39:00
tags: [C]
---
## 源代码下载
代码放到了github上，下面是下载地址与源码
{% copy https://github.com/Alanosy/git_study/blob/master/c/student_3.c %}

## 代码
```
//头文件
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
//#include <unistd.h> //mac调用命令的头文件
//#include <windows.h>  //windows调用命令的头文件
//宏定义
#define max_sub_num 30
//枚举类型
enum gender {male,female};
//生日结构题
typedef struct birthday
{
    int year;
    int month;
    int day;
}birthday;
//科目结构体
typedef struct subject
{
    char s[20];
    float score;
}subject;
//树存储结构
typedef struct tree
{
    int num;
//    char num[15];
    char name[10];
    char major[20];
    int grade;
    birthday birt;
    enum gender g;
    subject sub[max_sub_num];
    struct tree *rchild,*lchild;
}tr,*tree;
//目录
void menu()
{
    printf("………………欢迎使用学籍管理系统……………………\n");
    printf("………………     1.添加信息     ……………………\n");
    printf("………………     2.删除信息     ……………………\n");
    printf("………………     3.修改信息     ……………………\n");
    printf("………………     4.显示信息     ……………………\n");
    printf("………………     0.退出系统     ……………………\n");

}
//录入菜单
void input_menu()
{
    printf("姓名 专业 年级 年 月 日 性别（男：M，女：F）：\n");

}
//打印菜单
void print_menu()
{
    printf("学号 姓名 专业 年级 年 月 日 性别（男：M，女：F）：\n");
}
//查找存储位置
int find(tree T,int a,tree f,tree *p)
{
    if(!T)
    {
        (*p)=f;
        return 0;
    }
    else if((T->num)==a)
    {
        (*p)=T;
        return 1;
    }
    else if((T->num)<a)
    {
        return find(T->rchild,a,T,p);
    }
    else
    {
        return find(T->lchild,a,T,p);
    }
}
//录入数据
int add(tree *T)
{
    int b,i,n,a;
    char c;
    tree s;
    tree f,p;
    f=p=NULL;
    while(1)
    {
        printf("请输入学号：");
        scanf("%d",&a);
        if(!find((*T),a,f,&p))
        {
            s=(tree) malloc(sizeof (tr));
            s->num=a;
            input_menu();
            scanf("%s %s %d %d %d %d %c",s->name,s->major,&s->grade,&s->birt.year,&s->birt.month,&s->birt.day,&c);
            if(c=='M')
            {
                s->g=male;
            }
            else
                s->g=female;
            printf("请输入科目数量：");
            scanf("%d",&n);
            printf("输入科目-成绩：\n");
            for(i=0;i<n;i++)
            {
                scanf("%s %f",s->sub[i].s,&s->sub[i].score);
            }
            s->rchild=s->lchild=NULL;
            if(!p)
            {
                (*T)=s;
                (*T)->rchild=(*T)->lchild=NULL;
            }
            else if((p->num)<(s->num))
            {
                p->rchild=s;
            }
            else
            {
                p->lchild=s;
            }
        }
        getchar();
        printf("还要继续么(Y/N)？：");
        char s=getchar();
        switch (s) {
            case 'n': return 1;
            case 'N': return 1;
            case 'y': break;
            case 'Y': break;
            default: break;
        }
    }
}
//显示所有信息
void output(tree T)
{
    if(T!=NULL) {
        if(T->num!=0)
        {
            printf("%d    %s     %s    %d    %d    %d    %d    ",T->num,T->name, T->major, T->grade, T->birt.year, T->birt.month, T->birt.day);
            if (T->g == 0)
            {
                printf("male \n");
            }
            else
            {
                printf("female \n");
            }
            output(T->lchild);
            output(T->rchild);
        }
    }
}
//删除信息
int deletes(tree *p)
{
    tree temp,s;
    temp=s=NULL;
    if(((*p)->rchild==NULL)&&((*p)->lchild==NULL))
    {
        free(*p);
        return 0;
    }
    else if((*p)->lchild)
    {
        for(temp=(*p)->lchild;temp->rchild!=NULL;temp=temp->rchild);
        (*p)->num=temp->num;
        deletes(&((*p)->lchild));
        (*p)->lchild=NULL;
    }
    else
    {
        for(temp=(*p)->rchild;temp->lchild!=NULL;temp=temp->lchild);
        (*p)->num=temp->num;
        deletes(&((*p)->rchild));
        (*p)->rchild=NULL;
    }

    return 1;
}
//删除查找
int delete(tree *T,int a)
{
    if(!(*T))
    {
        printf("当前无信息\n");
        return 0;
    }
    else
    {
        if((*T)->num==a)
        {
            return deletes(&(*T));
        }
        else if((*T)->num<a)
        {
            return delete((*T)->rchild,a);
        }
        else
        {
            return delete((*T)->lchild,a);
        }

    }
}
//修改信息
int alters(tree *p)
{
    char c;
    int i,n;
    input_menu();
    scanf("%s %s %d %d %d %d %c",(*p)->name,(*p)->major,&(*p)->grade,&(*p)->birt.year,&(*p)->birt.month,&(*p)->birt.day,&c);
    if(c=='M')
    {
        (*p)->g=male;
    }
    else
        (*p)->g=female;
    printf("请输入科目数量：");
    scanf("%d",&n);
    printf("输入科目-成绩：\n");
    for(i=0;i<n;i++)
    {
        scanf("%s %f",(*p)->sub[i].s,&(*p)->sub[i].score);
    }
    return 1;
}
//修改判断
int alter(tree *T,int a)
{
    if(!(*T))
    {
        printf("当前无信息\n");
        return 0;
    }
    else
    {
        if((*T)->num==a)
        {
            return alters(&(*T));
        }
        else if((*T)->num<a)
        {
            return alter((*T)->rchild,a);
        }
        else
        {
            return alter((*T)->lchild,a);
        }

    }
}
//程序入口
int main()
{
    tree T=NULL;
    int choose,a;
    while (1)
    {
        menu();
        printf("请输入你的选择：");
        scanf("%d",&choose);
        switch (choose) {
            case 0:
            {
                exit(0);
            }
            case 1:
            {
                add(&T);
                printf("插入成功\n");
//                system("pause");
                break;
            }
            case 2:
            {
                printf("请输入学号：\n");
                scanf("%d",&a);
                delete(&T,a);
                printf("删除成功\n");
//                system("pause");
                break;
            }
            case 3:
            {
                printf("请输入学号：\n");
                scanf("%d",&a);
                alter(&T,a);
                printf("修改成功\n");
//                system("pause");
                break;
            }
            case 4:
            {
                print_menu();
                output(T);
                printf("显示成功\n");
//                system("pause");
                break;
            }
            default:
                break;
        }
    }
}
```