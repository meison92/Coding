# [LeetCode371.两整数之和](https://leetcode-cn.com/problems/sum-of-two-integers/)
## 题目描述
不使用运算符 `+` 和 `-` ​​​​​​​，计算两整数 `​​​​​a` 、`b` ​​​​​​​之和。

### 示例
```java
输入: a = 1, b = 2
输出: 3
```
```
输入: a = -2, b = 3
输出: 1
```
## 题解
我们可以用三步走的方式计算二进制值相加： 5---`101`，7---`111`

1. 第一步：相加各位的值，不算进位，得到`010`，二进制每位相加就相当于各位做异或操作，`101^111`。
2. 第二步：计算进位值，得到`1010`，相当于各位进行与操作得到`101`，再向左移一位得到`1010`，`(101&111)<<1`。
3. 第三步重复上述两步，各位相加 `010^1010=1000`，进位值为`100=(010 & 1010)<<1`。
4. 继续重复上述两步：`1000^100 = 1100`，进位值为`0`，跳出循环，`1100`为最终结果。
5. 结束条件：进位为`0`，即`a`为最终的求和结果。

```java
class Solution {
    public int getSum(int a, int b) {
        while(b!=0){
            int temp=a^b;
            b=(a&b)<<1;
            a=temp;
        }
        return a;
    }
}
```