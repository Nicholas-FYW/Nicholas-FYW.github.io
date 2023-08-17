# 问题 H 整数奇偶排序


#### 题目描述

输入10个整数，彼此以空格分隔。重新排序以后输出(也按空格分隔)，要求:
1.先输出其中的奇数,并按从大到小排列；
2.然后输出其中的偶数,并按从小到大排列。

#### 输入

任意排序的10个整数（0～100），彼此以空格分隔。

#### 输出

可能有多组测试数据，对于每组数据，按照要求排序后输出，由空格分隔。

#### 思路

使用双指针，分别对奇数和偶数进行划分，然后分别对奇数和偶数进行排序

#### 代码

````c++
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

int main()
{
    int n;
    vector<int> num(10);
    while (cin >> num[0])
    {
        for (int i = 1; i <= 9; i++)
        {
            cin >> num[i];
        }
        int i = 0, j = 9;
        while (i < j)
        {
            //每次结束排序时i指向的是一个奇数，j指向的是一个偶数，最后结束是i=j，因此i指向的是一个偶数
            while (i < j && num[i] % 2 != 0)
            {
                i++;
            }
            while (i < j && num[i] % 2 != 0)
            {
                j--;
            }
            swap(num[i], num[j]);
        }
        sort(num.begin(), num.begin() + i);
        reverse(num.begin(), num.begin() + i);
        sort(num.begin() + i, num.end());
        for (int i = 0; i < 10; i++)
        {
            printf("%d ", num[i]);
        }
        printf("\n");
    }
    return 0;
}
````


