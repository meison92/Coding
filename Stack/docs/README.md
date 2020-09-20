# [LeetCode739.每日温度](https://leetcode-cn.com/problems/daily-temperatures/)
## 题目描述
请根据每日 气温 列表，重新生成一个列表。对应位置的输出为：要想观测到更高的气温，至少需要等待的天数。如果气温在这之后都不会升高，请在该位置用 0 来代替。

例如，给定一个列表 `temperatures = [73, 74, 75, 71, 69, 72, 76, 73]`，你的输出应该是 `[1, 1, 4, 2, 1, 1, 0, 0]`。

提示：气温 列表长度的范围是 `[1, 30000]`。每个气温的值的均为华氏度，都是在 `[30, 100]` 范围内的整数。

## 题解
### 解法一
```java
class Solution {
    public int[] dailyTemperatures(int[] T) {
        Deque<Integer> stack=new LinkedList<>();
        int len=T.length;
        int[] ans=new int[len];
        for(int i=len-1;i>=0;i--){
            while(stack.isEmpty()==false&&T[stack.peek()]<=T[i]){
                stack.pollFirst();
            }
            if(stack.isEmpty()==true){
                ans[i]=0;
            }else{
                ans[i]=stack.peek()-i;
            }
            stack.offerFirst(i);
        }
        return ans;
    }
}
```
### 解法二
```java
class Solution {
    public int[] dailyTemperatures(int[] T) {
        if(T==null){
            return new int[0];
        }
        int len=T.length;
        if(len==1){
            return new int[]{0};
        }
        int[] ans=new int[len];
        for(int i=0;i<len;i++){
            ans[i]=0;
            for(int j=i+1;j<len;j++){
                if(T[j]>T[i]){
                    ans[i]=j-i;
                    break;
                }
            }
        }
        return ans;
    }
}
```