# 1048 数字加密


**1048 数字加密**

本题要求实现一种数字加密方法。首先固定一个加密用正整数 A，对任一正整数 B，将其每 1 位数字与 A 的对应位置上的数字进行以下运算：对奇数位，对应位的数字相加后对 13 取余——这里用 J 代表 10、Q 代表 11、K 代表 12；对偶数位，用 B 的数字减去 A 的数字，若结果为负数，则再加 10。这里令个位为第 1 位。

### 输入格式：

输入在一行中依次给出 A 和 B，均为不超过 100 位的正整数，其间以空格分隔。

### 输出格式：

在一行中输出加密后的结果。

### 输入样例：

```in
1234567 368782971
```

### 输出样例：

```out
3695Q8118
```

### 思路

  将A、B进行reverse，然后再进行加密

  首先取A、B里面的长度较小值，然后进行对应位加密

  最后倒序输出

```c++
#include <iostream>
#include <algorithm>
using namespace std;

/*
    将A、B进行reverse，然后再进行加密
    首先取A、B里面的长度较小值，然后进行对应位加密
    最后倒序输出 */

int main()
{
    string a, b;
    char arr[13] = {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'J', 'Q', 'K'};
    while (cin >> a >> b)
    {
        reverse(a.begin(), a.end());
        reverse(b.begin(), b.end());
        int len = min(a.size(), b.size());
        int num[1005];
        for (int i = 0; i < len; i++)
        {
            if ((i + 1) % 2 != 0)
            {
                num[i] = ((b[i] - '0') + (a[i] - '0')) % 13;
            }
            else
            {
                num[i] = (b[i] - '0') - (a[i] - '0');
                if (num[i] < 0)
                    num[i] += 10;
            }
        }
        int l = max(a.size(), b.size());
        if (a.size() > b.size())
        {
            for (int j = len; j < l; j++)
            {
                if ((j + 1) % 2 != 0)
                {
                    num[j] = (a[j] - '0') % 13;
                }
                else
                {
                    num[j] = 0 - (a[j] - '0');
                    if (num[j] < 0)
                        num[j] += 10;
                }
            }
        }
        else
        {
            for (int j = len; j < l; j++)
            {
                if ((j + 1) % 2 != 0)
                {
                    num[j] = (b[j] - '0') % 13;
                }
                else
                {
                    num[j] = b[j] - '0';
                }
            }
        }

        for (int i = l - 1; i >= 0; i--)
        {
            printf("%c", arr[num[i]]);
        }
    }
    return 0;
}
```



<!--more-->

