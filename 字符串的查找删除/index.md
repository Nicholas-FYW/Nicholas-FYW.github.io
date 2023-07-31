# 字符串的查找删除


#### 题目描述

给定一个短字符串（不含空格），再给定若干字符串，在这些字符串中删除所含有的短字符串。

#### 输入

输入只有1组数据。
输入一个短字符串（不含空格），再输入若干字符串直到文件结束为止。

#### 输出

删除输入的短字符串(不区分大小写)并去掉空格,输出。

#### 思路

利用string的find，earse进行操作，使用string一行一行进行接收，然后再进行处理，要求不区分大小写进行删除处理，我们可以把输入的string和短字符串全都变成小写，然后再把string和短字符串进行对比，同时将string的值进行复制，对复制后的值进行和小写的值做同样的处理。

首先先把string全部变成小写，然后再把string和短字符串进行对比，对string和复制后的字符串进行相同的处理，最后对string和复制后的字符串进行去掉空格的处理。

find(字符串， 起始位)

erase(起始位， 大小)

```c++
#include <iostream>
#include <cstring>
using namespace std;

int main()
{
    string t;
    getline(cin, t);
    int len = t.size();
    for (int i = 0; i < len; i++)
    {
        t[i] = tolower(t[i]);
    }
    string s1, s2;
    while (getline(cin, s1))
    {
        s2 = s1;
        int l = s1.size();
        //  turn string to lowcase
        for (int i = 0; i < l; i++)
        {
            s1[i] = tolower(s1[i]);
        }
        int tmp = s1.find(t, 0);
        //  del the short string
        while (tmp != string::npos)
        {
            s1.erase(tmp, len);
            s2.erase(tmp, len);
            tmp = s1.find(t, tmp);
        }
        tmp = s1.find(" ", 0);
        //  del spaces
        while (tmp != string::npos)
        {
            s1.erase(tmp, 1);
            s2.erase(tmp, 1);
            tmp = s1.find(" ", tmp);
        }
        cout << s2 << endl;
    }
    return 0;
}
```







<!--more-->

