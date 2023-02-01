---
layout: wiki  # 使用wiki布局模板
wiki: 学生成绩管理系统 # 这是项目名
title: 数组与链表学生成绩管理系统
---
## 引言

因为学生管理系统类似数据库，需要实现增删改查，来管理其数据，所以该管理系统也应该实现这四个功能，这里使用数组实现，且具体实现如下。  

## 源代码

具体源代码存放在gitee仓库地址如下  

{% copy https://gitee.com/thebyte/work.git %}

## 学生成绩管理系统之目录  

```
//菜单
void menu()
{
    printf("===============\n");
    printf("1、学生成绩录入\n");
    printf("2、学生成绩删除\n");
    printf("3、学生成绩修改\n");
    printf("4、学生成绩查询\n");
    printf("5、学生成绩打印\n");
    printf("6、排       序\n");
    printf("0、退       出\n");
    printf("===============\n");
}
```

这里使用printf()函数直接输出  

## 学生成绩管理系统之录入

```
//录入成绩
void add()
{

    for (int i = 0; i < max - actual;i++)
    {
        int temp,k=0;//temp用来存放学号
        //当数组有成绩时
        if (actual>0) {
            printf("请输入第%d位学生的学号为：", actual+1);
            scanf("%d", &temp);
            //判断是否有重复学号
            while (temp!=student[k][0]&&k<actual)
            {
                k++;
            }
            if(temp==student[k][0])
            {
                //如果在数组中找到相同学号，则跳出本次循环重新输入
                printf("学号重复请重新输入!\n");
                continue;
            }
            else
            {
                student[actual][0]=temp;
                printf("请输学号为%d的同学成绩：", student[actual][0]);
                scanf("%d", &student[actual][1]);
                actual++;

            }
            //判断是否继续
            getchar();
            printf("还有继续么(y/n):");
            char c = getchar();
            if (c == 'y' || c == 'Y')
            {
                ;
            }
            else if (c == 'n' || c == 'N')
            {
                break;
            }
            else
            {
                printf("输入错误，即将退出录入系统!\n");
                break;
            }
            }
            //当数组没有成绩时
            else if (actual==0) {
            printf("请输入第%d位学生的学号为：", i + 1);
            scanf("%d", &temp);
            //查找并判断是否有重复的学号
            while (temp!=student[k][0]&&k<actual)
            {
                k++;
            }
            if(temp==student[k][0])
            {
                //如果在数组中找到相同学号，则跳出本次循环重新输入
                printf("学号重复请重新输入!\n");
                continue;
            }
            else
            {
                student[i][0]=temp;
                printf("请输学号为%d的同学成绩：", student[i][0]);
                scanf("%d", &student[i][1]);
                actual++;

            }
            getchar();
            printf("还有继续么(y/n):");
            char c = getchar();
            if (c == 'y' || c == 'Y') { ;
            } else if (c == 'n' || c == 'N') {
                break;
            } else {
                printf("输入错误，即将退出录入系统!\n");
                break;
            }
        }


    }
}
```
这里需要定义一个二维数组，将学号放第一列，成绩放低0列，还需用到循环与条件判断来判断是否还要继续输入,并且定义一个存放实际人数变量actual，每次录入加1人  

## 学习管理系统之修改

```
//修改成绩
void alter() {
    while (1) {
        int number, i = 0;
        //输入要修改成绩的学号
        printf("请输入要修改的学号：");
        scanf("%d", &number);
        //开始查找与学号配对的成绩位置
        while (number != student[i][0] && i < actual)
        {
            i++;
        }
        //判断是否有该学号的成绩
        if (number == student[i][0])
        {
            //有该学号则输入修改后的成绩
            printf("请输入要修改的成绩：");
            scanf("%d", &student[i][1]);
        }
        else
        {
            //没有则输出查无此人
            printf("查无此人\n");
        }
        //判断是否继续修改
        getchar();
        printf("还有继续么(y/n)：");
        char c = getchar();
        if (c == 'y' || c == 'Y')
        {
            ;
        }
        else if (c == 'n' || c == 'N')
        {
            break;
        }
        else
        {
            printf("输入错误，即将退出修改系统!\n");
        }

    }
}

```
这里使用循环一个一个学号对比，找到后然后将修改成绩覆盖到要修改的成绩位置，没找到则输出查无此人  

## 学生成绩管理系统之删除

```
//删除成绩
void delete()
{
    while (1) {
        int number, i = 0;
        //输入要删除成绩的学号
        printf("请输入要删除成绩的学号：");
        scanf("%d", &number);
        //查找学号
        while (number != student[i][0] && i < actual)
        {
            i++;
        }
        //判断是否有此学号
        if (number == student[i][0])
        {
            //如果有，则后面的成绩覆盖要删除的成绩，后面依次往前挪
            for(;i<actual;i++)
            {
                student[i][0]=student[i+1][0];
                student[i][1]=student[i+1][1];

            }
            printf("删除成功!\n");
        }
        else
        {
            //如果没有，则输出查无此人
            printf("查无此人!\n");
        }
        //删除一个成绩则实际人数减一
        actual--;
        //判断是否继续删除
        getchar();
        printf("还有继续么(y/n)：");
        char c = getchar();
        if (c == 'y' || c == 'Y')
        {
            //如果输入为y则执行空语句
            ;
        }
        else if (c == 'n' || c == 'N')
        {
            break;
        }
        else
        {
            printf("输入错误，即将退出删除系统!\n");
            break;

        }

    }
}
```
删除类似修改，只是将成绩覆盖改成，下面的成绩全部往上移1格，这里每删除一个人则实际人数actual减1人  

## 学生成绩管理系统之查找

```
void find()
{
    while (1) {

        int number, i = 0;
        //输入要查找成绩的学号
        printf("请输入要查找的学号：");
        scanf("%d", &number);
        //查找学号对应的成绩位置
        while (number != student[i][0] && i < actual)
        {
            i++;
        }
        //判断是否有与之对应的学号
        if (number == student[i][0])
        {
            //有则输出成绩
            printf("学号为%d的成绩为：%d\n",number,student[i][1]);
        }
        else
        {
            //没有则输出查无此人
            printf("查无此人\n");
        }
        //判断是否继续
        getchar();
        printf("还有继续么(y/n)：");
        char c = getchar();
        if (c == 'y' || c == 'Y')
        {
            ;
        }
        else if (c == 'n' || c == 'N')
        {
            break;
        }
        else
        {
            printf("输入错误，即将退出查找系统\n");

        }

    }

}
```
查找也是利用学号，一一对比找学号，然后打印该学号位置的成绩  

## 学生成绩管理系统之打印
```
void print()
{
    //用for循环依次打印出实际人数的学号成绩对应表
    int i;
    printf("成绩表如下（学号-成绩）：\n");
    for(i=0;i<actual;i++)
    {
        printf("%4d%4d\n",student[i][0],student[i][1]);
    }
    float average=0.0;
    float sum=0.0;
    for(int j=0;j<actual;j++)
    {
        sum=sum+student[j][1];
    }
    average=sum/actual;
    printf("全班的平均成绩为%2f\n",average);
}

```
这里使用for循环一一换行打印  

## 学生成绩管理系统之排序
### 冒泡排序
```
void maopao()
{
    int temp=0,num=0;                               //初始化存放成绩和学号的临时变量
    for(int i=0;i<actual-1;i++)                     //遍历实际人数-1次
    {
        for(int j=0;j<actual-i-1;j++)               //遍历实际人数减-1-1次；2人一组对比所以比要再减1次
        {
            if(student[j][1]>student[j+1][1])       //判断前后两数的大小，如果前面的成绩比后面成绩大
            {
                //交换成绩
                temp=student[j][1];
                student[j][1]= student[j+1][1];
                student[j+1][1]=temp;
                //交换学号
                num=student[j][0];
                student[j][0]=student[j+1][0];
                student[j+1][0]=num;
            }
        }
    }
    print();                           //打印成绩
}
```
两两比对，交换位置，然后循环重新再比对，注意点是，外循环与内循环都比实际人数少1位  

### 选择排序
```
//选择排序
void choice()
{
    int a=0,b=0,min;
    for(int i=0;i<actual-1;i++)
    {
        min=i;                          //假设最小值位置
        for(int j=i+1;j<actual;j++)     //开始遍历找所有的值对比
        {
            if(student[j][1]<student[min][1])       //如果后面的数小于最小值，则记录最小值的位置
            {
                min=j;
            }
        }
        if(min!=i)                      //如果最小值不等于最开始的位置，则
        {
            //交换学号
            b=student[min][0];
            student[min][0]=student[i][0];
            student[i][0]=b;
            //交换成绩
            a=student[min][1];
            student[min][1]=student[i][1];
            student[i][1]=a;

        }
    }
    print();                              //打印成绩
}
```
选择排序是将最小的元素挑出来与没排序的第一位交换位置，它会不断的选择剩余元素中的最小者      

### 插入排序
```
//插入排序
void insert()
{

    int i,j;
    int temp,id;
    for(i=1;i<actual;i++)
    {
        if(student[i][1]<student[i-1][1])           //如果后面的数小于前面的数
        {
            temp=student[i][1];                     //保存后面的数到temp
            id=student[i][0];                       //对应的学号保存到ou
            for(j=i-1;student[j][1]>temp;j--)       //开始将前面到数移位，当前面的数大于temp就开始循环，直到有比temp大的数和最前面则跳出循环
            {
                student[j+1][1]=student[j][1];      //将成绩向后移
                student[j+1][0]=student[j][0];      //学号向后移
                if(j<0)                             //当最小到数移动到第一位后
                {
                    break;                          //退出循环
                }
            }
            student[j+1][1]=temp;                     //将temp的值插入到比temp大的数的前面
            student[j+1][0]=id;                       //将对应的学号插入到对应的位置

        }
    }
    print();
}
```
插入在比自己小的数的前面  
首先将后面比前面小的数存放在另一个变量，然后前面比这个数大的数依次往后挪，直到比自己小的数，然后放入到其后面。  
### 归并排序
```
//归并排序
//分治  递归
void merge_split(){
    split(student,1,actual);
    print();
}
//将数组用递归拆成单个元素
void split(int arr[][2],int p,int q)
{
    int mid;
    //确保拆成单个元素
    if(arr== NULL ||p>q||p==q)
    {
        return ;
    }
    mid=(p+q)/2;
    split(arr,p,mid);
    split(arr,mid+1,q);
    merge(arr,p,mid,q);
}
//排序归并在一起
void merge(int arr[][2],int p,int mid,int q){
    int i,j,k;
    int L,R;
    //定义临时存放左右数组的数组
    int LL[max][2];
    int RR[max][2];
    //定义左右数组长度
    L=mid-p+1;
    R=q-mid;
    //将左边数组存放到临时数组
    for(i=0;i<L;i++)
    {
        LL[i][1]=arr[p-1+i][1];
        LL[i][0]=arr[p-1+i][0];
    }
    //将右边数组存放到临时数组
    for(i=0;i<R;i++)
    {
        RR[i][1]=arr[mid+i][1];
        RR[i][0]=arr[mid+i][0];
    }
    i=0;
    j=0;
    for(k=p;k<=q;k++)
    {
        //当LL与RR没有元素时，放入原来数组
        if(i==L)
        {
            arr[k-1][1]=RR[j][1];
            arr[k-1][0]=RR[j][0];
            j++;

        }
        else if(j==R)
        {
            arr[k-1][1]=LL[i][1];
            arr[k-1][0]=LL[i][0];
            i++;
        }
        else
        {
            //当LL与RR还有元素时，放入原来数组
            if(LL[i][1]<RR[j][1])
            {
                arr[k-1][1]=LL[i][1];
                arr[k-1][0]=LL[i][0];
                i++;
            }
            else
            {
                arr[k-1][1]=RR[j][1];
                arr[k-1][0]=RR[j][0];
                j++;
            }
        }
    }
}
```
先用递归拆分数组，然后用循环归并并排序数组  
递归是不断把数组拆成左右两部分，其中写的if判断是用来限制，分成一个元素后不可再分。
归并是先记录左右素组的大小，然后分别放到另一个数组中，然后归并到原来的数组，分别对左右数组的第一个元素比较  
当剩下元素没用完时会添加再数组后面

## 功能选择
### 功能选择
```
int select()
{
    while (1)
    {
        int i;
        menu();
        printf("请输入要选择的功能：");
        scanf("%d",&i);
        switch (i)
        {
            case 1: add();break;
            case 2: delete();break;
            case 3: alter();break;
            case 4: find();break;
            case 5: print();break;
            case 6: short_1();break;
            case 0: return 0;
            default: printf("输入错误，请重新输入");break;
        }
    }
}
```
这里将多个函数封装到了功能选择函数中  
用switch来实现多种功能的选择  

### 排序选择
```
//排序算法目录
int short_1()
{
        int i;
        printf("===============\n");
        printf("1、冒泡排序\n");
        printf("2、选择排序\n");
        printf("3、插入排序\n");
        printf("4、归并排序\n");
        printf("===============\n");
        printf("请输入要使用的排序方法：");
        scanf("%d",&i);
        switch (i) {
            case 1: maopao();break;
            case 2: choice();break;
            case 3: insert();break;
            case 4: merge_split();break;
            default: printf("输入错误，请重新输入");break;

        }

}
```
与功能选择类似  

## 函数的入口main
```
int main() {
    select();
}
```
所有内容都是在main函数中使用的，所以要在main中导入之前的函数

## 源代码
具体源代码存放在gitee仓库地址如下  

{% copy https://gitee.com/thebyte/work.git %}

## 目录
目录就不用多说，用以前的打印就好了  
```
void menu()
{
    printf("===============\n");
    printf("1、学生成绩录入\n");
    printf("2、学生成绩删除\n");
    printf("3、学生成绩修改\n");
    printf("4、学生成绩查询\n");
    printf("5、学生成绩打印\n");
    printf("6、释 放 空 间\n");
    printf("0、退       出\n");
    printf("===============\n");
}
```
## 链表录入
先要定义结构体  
```
typedef struct student
{
    //信息域
    int num;
    char name[10];
    char sex;
    float score;
    //指针域
    struct student *next;
}stu;
```
然后需要定义头指针  
```
stu *head=NULL;
```
然后开始判断链表是否为空  
```
void add()
{
    //定义选择变量
    int choose;
    //定义尾指针
    stu *last=NULL;
    while (1)
    {
        //当链表为空时，head当next成员指向last，last为新节点，用来存放数据，last当next成员指向空
        if(head==NULL)
        {
            //给第一个节点分配空间，当链表只有一个节点时，这个节点就是这个链表当last
            last=(stu *)malloc(sizeof (stu));
            last->next=NULL;
            head=(stu *)malloc(sizeof (stu));
            head->next=last;
            //录入信息到信息域
            printf("请输入学号：");
            scanf("%d",&last->num);
            printf("请输入姓名：");
            scanf("%s",last->name);
            getchar();
            printf("请输入性别（男:M,女:F)：");
            scanf("%c",&last->sex);
            printf("请输入成绩：");
            scanf("%f",&last->score);
        }
        //当链表不为空时，找到最后一个节点，last的next成员分配空间，然后最新的将last这个指针指向刚刚建立的空间为最新的last，然后最新的last的next成员指向null
        else if(head!=NULL)
        {
            //查找链表的最后一个节点
            last=head->next;
            while(last->next!=NULL)
            {
                last=last->next;
            }
            //分配新节点空间
            last->next=(stu *)malloc(sizeof (stu));
            //标注新的last
            last=last->next;
            last->next=NULL;
            //录入信息到信息域
            printf("请输入学号：");
            scanf("%d",&last->num);
            printf("请输入姓名：");
            scanf("%s",last->name);
            getchar();
            printf("请输入性别（男:M,女:F)：");
            scanf("%c",&last->sex);
            printf("请输入成绩：");
            scanf("%f",&last->score);
        }
        getchar();
        printf("还有继续么(y/n)：");
        char c = getchar();
        if (c == 'y' || c == 'Y')
        {
            //如果输入为y则执行空语句
            ;
        }
        else if (c == 'n' || c == 'N')
        {
            break;
        }
        else
        {
            printf("输入错误，即将退出删除系统!\n");
            break;

        }
    }
}
```
其中也需要定义last尾指针，这个指针在录入时代表的意思是存放最后一个节点的地址  
其中malloc()内存分配函数需要强行改变类型切需要引用头文件  
```
#include <stdlib.h>
```

## 删除成绩
删除后面的都依照数组实现的学生管理系统逻辑推理写出，就不过多解释，有不懂的可以在联系我
```
void delete()
{
    while (1)
    {
        int num;
        if(head==NULL)
        {
            printf("学生成绩表无信息\n");
            break;
        }
        printf("请输入要删除成绩的学号：");
        scanf("%d",&num);
        stu *temp;
        temp=head;
        while(temp->next!=NULL)
        {
            if(num==temp->next->num)
            {
                stu *del=temp->next;
                temp->next=temp->next->next;
                free(del);
                break;
            }
            temp=temp->next;
        }
        if(temp==NULL)
        {
            printf("查无此人");
        }

        getchar();
        printf("还有继续么(y/n)：");
        char c = getchar();
        if (c == 'y' || c == 'Y')
        {
            //如果输入为y则执行空语句
            ;
        }
        else if (c == 'n' || c == 'N')
        {
            break;
        }
        else
        {
            printf("输入错误，即将退出删除系统!\n");
            break;

        }
    }
}
```
## 修改成绩
```
//修改成绩
void alter()
{
    while (1)
    {
        int num;
        if(head==NULL)
        {
            printf("学生成绩表无信息\n");
            break;
        }
        printf("请输入要修改成绩的学号：");
        scanf("%d",&num);
        stu *temp;
        temp=head->next;
        while(temp!=NULL)
        {
            if(num==temp->num)
            {
                printf("请输入要修改的成绩：");
                scanf("%f",&temp->score);
                break;
            }
            temp=temp->next;
        }
        if(temp==NULL)
        {
            printf("查无此人");
        }

        getchar();
        printf("还有继续么(y/n)：");
        char c = getchar();
        if (c == 'y' || c == 'Y')
        {
            //如果输入为y则执行空语句
            ;
        }
        else if (c == 'n' || c == 'N')
        {
            break;
        }
        else
        {
            printf("输入错误，即将退出删除系统!\n");
            break;

        }
    }
}
```
## 打印链表
```
//链表当输出
void print()
{
    stu *temp;
    temp=head->next;
    printf("学号\t\t\t\t姓名\t\t性别\t\t成绩\n");
    while(temp!=NULL)
    {
        printf("%-16d%-8s%-8c%-8.2f\n",temp->num,temp->name,temp->sex,temp->score);
        temp=temp->next;
    }
    return;

}
```
## 释放内存空间
```
//释放空间
void release()
{
    stu *temp_2;
    while(head!=NULL)
    {
        temp_2=head;
        head=head->next;
        free(temp_2);
    }

}
```
## 成绩查询
```
//查找成绩
void find()
{
    while (1)
    {
        int num;
        if(head==NULL)
        {
            printf("学生成绩表无信息\n");
            break;
        }
        printf("请输入要查找的学号：");
        scanf("%d",&num);
        stu *temp;
        temp=head->next;
        while(temp!=NULL)
        {
            if(num==temp->num)
            {
                printf("你要查找的学生信息如下：\n");
                printf("学号\t\t\t\t姓名\t\t性别\t\t成绩\n");
                printf("%-16d%-8s%-8c%-8.2f\n",temp->num,temp->name,temp->sex,temp->score);
                break;
            }
            temp=temp->next;
        }
        if(temp==NULL)
        {
            printf("查无此人");
        }

        getchar();
        printf("还有继续么(y/n)：");
        char c = getchar();
        if (c == 'y' || c == 'Y')
        {
            //如果输入为y则执行空语句
            ;
        }
        else if (c == 'n' || c == 'N')
        {
            break;
        }
        else
        {
            printf("输入错误，即将退出删除系统!\n");
            break;

        }
    }
}
```
## 功能选择与程序入口
```
//选择功能
int select()
{
    while (1)
    {
        int i;
        menu();
        printf("请输入要选择的功能：");
        scanf("%d",&i);
        switch (i)
        {
            case 1: add();break;
            case 2: delete();break;
            case 3: alter();break;
            case 4: find();break;
            case 5: print();break;
            case 6: release();break;
            case 0: return 0;
            default: printf("输入错误，请重新输入");break;
        }
    }
}
int main()
{
    select();
}
```