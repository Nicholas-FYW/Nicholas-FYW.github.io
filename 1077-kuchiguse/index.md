# 2


The Japanese language is notorious for its sentence ending particles. Personal preference of such particles can be considered as a reflection of the speaker's personality. Such a preference is called "Kuchiguse" and is often exaggerated artistically in Anime and Manga. For example, the artificial sentence ending particle "nyan~" is often used as a stereotype for characters with a cat-like personality:

- Itai nyan~ (It hurts, nyan~)
- Ninjin wa iyada nyan~ (I hate carrots, nyan~)

Now given a few lines spoken by the same character, can you find her Kuchiguse?

### Input Specification:

Each input file contains one test case. For each case, the first line is an integer *N* (2≤*N*≤100). Following are *N* file lines of 0~256 (inclusive) characters in length, each representing a character's spoken line. The spoken lines are case sensitive.

### Output Specification:

For each test case, print in one line the kuchiguse of the character, i.e., the longest common suffix of all *N* lines. If there is no such suffix, write `nai`.

### Sample Input 1:

```in
3
Itai nyan~
Ninjin wa iyadanyan~
uhhh nyan~
```

### Sample Output 1:

```out
nyan~
```

### Sample Input 2:

```in
3
Itai!
Ninjinnwaiyada T_T
T_T
```

### Sample Output 2:

```out
nai
```

### 思路

  使用字符串进行输入的时候空格会结束输入

  寻找最长后缀匹配不太方便，我们可以对它进行变换

  转变为寻找最长前缀匹配

  首先，对所有的字符串进行reverse

  然后再将第一个字符串的每个单词和其他所有的字符串进行比较，

  发现出现不一样的单词就停止进行比对

```
#include <iostream>
#include <algorithm>
using namespace std;

/*
    使用字符串进行输入的时候空格会结束输入
    寻找最长后缀匹配不太方便，我们可以对它进行变换
    转变为寻找最长前缀匹配
    首先，对所有的字符串进行reverse
    然后再将第一个字符串的每个单词和其他所有的字符串进行比较，
    发现出现不一样的单词就停止进行比对
     */

int main()
{
    int n;
    string sen[1005];
    while (scanf("%d", &n) != EOF)
    {
        getchar();
        for (int i = 0; i < n; i++)
        {
            getline(cin, sen[i]);
            reverse(sen[i].begin(), sen[i].end());
        }
        int len = sen[0].size(), flag = 0, index = 0;
        for (int i = 0; i < len; i++)
        {
            char c = sen[0][i];
            for (int j = 1; j < n; j++)
            {
                if (sen[j][i] != c)
                {
                    flag = 1;
                    break;
                }
            }
            if (flag)
            {
                index = i - 1;
                break;
            }
        }
        if (index < 0)
        {
            printf("nai");
        }
        else
        {
            for (int i = index; i >= 0; i--)
            {
                printf("%c", sen[0][i]);
            }
        }

        printf("\n");
    }
    return 0;
}
```





<!--more-->

