### 题目描述
实现 `strStr()` 函数。
给定一个 `haystack` 字符串和一个 `needle` 字符串，在 `haystack`字符串中找出
 `needle` 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。

### 示例  
**示例1:**
```
输入: haystack = "hello", needle = "ll"
输出: 2
```
**示例2:**
```
输入: haystack = "aaaaa", needle = "bba"
输出: -1
```

### 说明
当 `needle` 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好
的问题。对于本题而言，当 `needle` 是空字符串时我们应当返回` 0` 。这
与C语言的 `strstr() `以及 Java的` indexOf() `定义相符。

### 题解  
#### 解法一、28.实现 strStr()用JAVA语言实现
```
class Solution {
    public int strStr(String haystack, String needle) {
        int index = -1;
        if(needle.length() == 0){
            index = 0;
        }else{
            index = haystack.indexOf(needle);
        }
        return index;
    }
}
```
#### 解法二、用Java语言编写
**本解法使用二分法进行查找**
一个数的平方根一定不大于他自己的一半，所以可以直接吧范围缩小一半，然后在这一半的元素里面找到中间位置的一个，计算出他的平方，然后跟原数比较，太大说明中位数比原来的那个数的平方根大，所以接下来选择中位数左边的区间，反之选择右边的区间。重复上面的步骤直到剩下最后一个数为止
```
class Solution {
    public int mySqrt(int x) {
        long right = x/2+1;
        long left = 0;
        while(left < right){
            long mid = (left+right)/2+1;
            long squar = mid*mid;
            if(squar > x){
                right=mid-1;
            }else{
                left=mid;
            }
        }
        return (int)left;
    }
}
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/implement-strstr
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。