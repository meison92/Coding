# [剑指Offer58-II.左旋转字符串](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)
## 题目描述
字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串`"abcdefg"`和数字2，该函数将返回左旋转两位得到的结果`"cdefgab"`。

- `1 <= k < s.length <= 10000`
### 示例
```
输入: s = "abcdefg", k = 2
输出: "cdefgab"
```
```
输入: s = "lrloseumgh", k = 6
输出: "umghlrlose"
```
## 题解
### 解法一
```java
class Solution {
    public String reverseLeftWords(String s, int n) {
        return s.substring(n, s.length()) + s.substring(0, n);
    }
}
```
### 解法二
```java
class Solution {
    public String reverseLeftWords(String s, int n) {
        StringBuilder res = new StringBuilder();
        for(int i = n; i < s.length(); i++)
            res.append(s.charAt(i));
        for(int i = 0; i < n; i++)
            res.append(s.charAt(i));
        return res.toString();
    }
}
```
### 解法三
```java
class Solution {
    public String reverseLeftWords(String s, int n) {
        char[] chs=s.toCharArray();
        reverseHelper(chs,0,n-1);
        reverseHelper(chs,n,s.length()-1);
        reverseHelper(chs,0,s.length()-1);
        return new String(chs);
    }
    public void reverseHelper(char[] chs,int start,int end){
        while(start<end){
            char temp=chs[start];
            chs[start]=chs[end];
            chs[end]=temp;
            start++;
            end--;
        }
    }
}
```