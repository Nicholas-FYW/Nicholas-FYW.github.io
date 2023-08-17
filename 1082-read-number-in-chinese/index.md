# 1082 Read Number in Chinese


Given an integer with no more than 9 digits, you are supposed to read it in the traditional Chinese way. Output `Fu` first if it is negative. For example, -123456789 is read as `Fu yi Yi er Qian san Bai si Shi wu Wan liu Qian qi Bai ba Shi jiu`. Note: zero (`ling`) must be handled correctly according to the Chinese tradition. For example, 100800 is `yi Shi Wan ling ba Bai`.

### Input Specification:

Each input file contains one test case, which gives an integer with no more than 9 digits.

### Output Specification:

For each test case, print in a line the Chinese way of reading the number. The characters are separated by a space and there must be no extra space at the end of the line.

### Sample Input 1:

```in
-123456789
```

### Sample Output 1:

```out
Fu yi Yi er Qian san Bai si Shi wu Wan liu Qian qi Bai ba Shi jiu
```

### Sample Input 2:

```in
100800
```

### Sample Output 2:

```out
yi Shi Wan ling ba Bai
```

### 思路

  分情况讨论：要做到不重不漏

  A&&B一共会出现四种情况

  A：T  B：T

  A：T  B：F

  A：F  B：T

  A：F  B：F

  使用两个数组分别去存储数字的汉字和单位

  为了保证按照格式输出首先输出最高位，然后再空格输出下一位

  输出接下来的数字时，当数字不为零时，输出它的数字和单位

  当数字为零时：数字所在单位代表的进制:如果数字所在单位的所有位不全为   零，输出进制

  零的输出:只要零后面还有零就需要输出零，连续的零只需要输出一个零

```c++
#include <iostream>
using namespace std;

/*
    分情况讨论：要做到不重不漏
    A&&B一共会出现四种情况
    A：T  B：T
    A：T  B：F
    A：F  B：T
    A：F  B：F
    使用两个数组分别去存储数字的汉字和单位
    为了保证按照格式输出首先输出最高位，然后再空格输出下一位
    输出接下来的数字时，当数字不为零时，输出它的数字和单位
    当数字为零时：数字所在单位代表的进制:如果数字所在单位的所有位不全为零，输出进制
    零的输出:只要零后面还有零就需要输出零，连续的零只需要输出一个零*/

int main()
{
    int n;
    string arr1[10] = {
        "ling", "yi", "er", "san", "si", "wu", "liu", "qi", "ba", "jiu"};
    string arr2[9] = {"", "Shi", "Bai", "Qian", "Wan", "Shi", "Bai", "Qian", "Yi"};
    while (scanf("%d", &n) != EOF)
    {
        int flag = 0;
        if (n < 0)
        {
            n = -n;
            flag = 1;
        }
        int num[20], index = 0;
        do
        {
            num[index++] = n % 10;
            n = n / 10;
        } while (n != 0);
        if (flag)
            printf("Fu ");
        printf("%s", arr1[num[index - 1]].c_str());
        if (index != 1)  printf(" %s", arr2[index - 1].c_str());
        int flag1 = 0, count = 0;
        for (int i = index - 2; i >= 0; i--)
        {
            if (num[i] == 0)
            {
                flag1 = 1;
                count++;
                //万进制的输出，描述不太准确：只要万进制的位不全为零，就要输出万
                if (i == 4)  printf(" %s", arr2[i].c_str());
                continue;
            }
            if (flag1)
            {
                printf(" ling");
                flag1 = 0;
                count = 0;
            }
            printf(" %s", arr1[num[i]].c_str());
            if (i != 0)  printf(" %s", arr2[i].c_str());
        }
    }
    return 0;
}
```



<!--more-->

