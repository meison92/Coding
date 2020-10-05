# [LeetCode179.最大数](https://leetcode-cn.com/problems/largest-number/)
## 题目描述
给定一组非负整数 `nums`，重新排列它们每位数字的顺序使之组成一个最大的整数。

注意：输出结果可能非常大，所以你需要返回一个字符串而不是整数。

- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 109`

### 示例
```
输入：nums = [10,2]
输出："210"
```
```
输入：nums = [3,30,34,5,9]
输出："9534330"
```
```
输入：nums = [1]
输出："1"
```
```
输入：nums = [10]
输出："10"
```
## 题解
为了构建最大数字，我们希望越高位的数字越大越好。

首先，我们将每个整数变成字符串。然后进行排序。

如果仅按降序排序，有相同的开头数字的时候会出现问题。比方说，样例 2 按降序排序得到的数字是 953433039 ，然而交换 3 和 30 的位置可以得到正确答案 9534330 。因此，每一对数在排序的比较过程中，我们比较两种连接顺序哪一种更好。我们可以证明这样的做法是正确的：

![](https://picgp.oss-cn-beijing.aliyuncs.com/img/20201005224339.png)

一旦数组排好了序，最“重要”的数字会在最前面。有一个需要注意的情况是如果数组只包含 0 ，我们直接返回结果 0 即可。否则，我们用排好序的数组形成一个字符串并返回。

```java
class Solution {
    public String largestNumber(int[] nums) {
        // Get input integers as strings.
        String[] asStrs = new String[nums.length];
        for (int i = 0; i < nums.length; i++) {
            asStrs[i] = String.valueOf(nums[i]);
        }

        // Sort strings according to custom comparator.
        Arrays.sort(asStrs,new Comparator<String>(){
            public int compare(String a,String b){
                String order1=a+b;
                String order2=b+a;
                return order2.compareTo(order1);
            }
        });

        // If, after being sorted, the largest number is `0`, the entire number
        // is zero.
        if (asStrs[0].equals("0")) {
            return "0";
        }

        // Build largest number from sorted array.
        String largestNumberStr = new String();
        for (String numAsStr : asStrs) {
            largestNumberStr += numAsStr;
        }

        return largestNumberStr;
    }
}
```
### 复杂度分析
- 时间复杂度：$O(nlgn)$,尽管我们在比较函数中做了一些额外的工作，但是这只是一个常数因子。所以总的时间复杂度是由排序决定的。
- 空间复杂度：$O(n)$,这里，我们使用了 $O(n)$ 的额外空间去保存 `nums` 的副本。尽管我们就地进行了一些额外的工作，但最后返回的数组需要 $O(n)$ 的空间。因此，需要的额外空间与 `nums` 大小成线性关系。

