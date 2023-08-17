# 1015 德才论


宋代史学家司马光在《资治通鉴》中有一段著名的“德才论”：“是故才德全尽谓之圣人，才德兼亡谓之愚人，德胜才谓之君子，才胜德谓之小人。凡取人之术，苟不得圣人，君子而与之，与其得小人，不若得愚人。”

现给出一批考生的德才分数，请根据司马光的理论给出录取排名。

### 输入格式：

输入第一行给出 3 个正整数，分别为：*N*（≤105），即考生总数；*L*（≥60），为录取最低分数线，即德分和才分均不低于 *L* 的考生才有资格被考虑录取；*H*（<100），为优先录取线——德分和才分均不低于此线的被定义为“才德全尽”，此类考生按德才总分从高到低排序；才分不到但德分到优先录取线的一类考生属于“德胜才”，也按总分排序，但排在第一类考生之后；德才分均低于 *H*，但是德分不低于才分的考生属于“才德兼亡”但尚有“德胜才”者，按总分排序，但排在第二类考生之后；其他达到最低线 *L* 的考生也按总分排序，但排在第三类考生之后。

随后 *N* 行，每行给出一位考生的信息，包括：`准考证号 德分 才分`，其中`准考证号`为 8 位整数，德才分为区间 [0, 100] 内的整数。数字间以空格分隔。

### 输出格式：

输出第一行首先给出达到最低分数线的考生人数 *M*，随后 *M* 行，每行按照输入格式输出一位考生的信息，考生按输入中说明的规则从高到低排序。当某类考生中有多人总分相同时，按其德分降序排列；若德分也并列，则按准考证号的升序输出。

### 输入样例：

```in
14 60 80
10000001 64 90
10000002 90 60
10000011 85 80
10000003 85 80
10000004 80 85
10000005 82 77
10000006 83 76
10000007 90 78
10000008 75 79
10000009 59 90
10000010 88 45
10000012 80 100
10000013 90 99
10000014 66 60
```

### 输出样例：

```out
12
10000013 90 99
10000012 80 100
10000003 85 80
10000011 85 80
10000004 80 85
10000007 90 78
10000006 83 76
10000005 82 77
10000002 90 60
10000014 66 60
10000008 75 79
10000001 64 90
```

### 思路

首先对第一种情况进行判断，当不满足时再对第二种情况进行判断

````c++
//坏情况
bool cmp(inf a, inf b)
{
    if (a.flag == b.flag)
    {
        int sum1, sum2;
        sum1 = a.virtue + a.talent;
        sum2 = b.virtue + b.virtue;
        if (sum1 == sum2)
        {
            if (a.virtue == b.virtue)  return strcmp(a.num, b.num) < 0;
            return a.virtue > b.virtue;
        }
        return sum1 > sum2;
    }
    return a.flag > b.flag;

}
````



```c++
#include <iostream>
#include <algorithm>
#include <cstring>
#include <vector>
using namespace std;

/*
    使用一个结构体来存储考生的信息，使用flag来存储考生的分类，
    当对学生进行排序的时候，首先判断按照分类进行排序，同一分类
    里面按照的是总分进行排序。
*/

struct inf
{
    char num[20];
    int virtue;
    int talent;
    int flag;
};

bool cmp(inf a, inf b)
{
    int sum1 = a.virtue + a.talent, sum2 = b.virtue + b.talent;
    if (a.flag != b.flag)  return a.flag < b.flag;
    else if (sum1 != sum2)  return sum1 > sum2;
    else if (a.virtue != b.virtue)  return a.virtue > b.virtue;
    return strcmp(a.num, b.num) < 0;
}

int main()
{
    int n, l, h;
    inf *data = new inf[100005];
    scanf("%d%d%d", &n, &l, &h);
    int count = n;
    for (int i = 0; i < n; i++)
    {
        scanf("%s%d%d", data[i].num, &data[i].virtue, &data[i].talent);

        if (data[i].virtue < l || data[i].talent < l)
        {
            data[i].flag = 0;
            count--;
        }
        else if (data[i].virtue >= h && data[i].talent >= h)
        {
            data[i].flag = 1;
        }
        else if (data[i].virtue >= h && data[i].talent < h)
        {
            data[i].flag = 2;
        }
        else if (data[i].virtue < h && data[i].talent < h && data[i].virtue >= data[i].talent)
        {
            data[i].flag = 3;
        }
        else
        {
            data[i].flag = 4;
        }
    }
        sort(data, data + n, cmp);
        printf("%d\n", count);
        for (int i = 0; i < n; i++)
        {
            if (!data[i].flag)
                continue;
            printf("%s %d %d", data[i].num, data[i].virtue, data[i].talent);
            if (i != n - 1)
                printf("\n");
        }
        delete[] data;
        return 0;
    }

```



<!--more-->

