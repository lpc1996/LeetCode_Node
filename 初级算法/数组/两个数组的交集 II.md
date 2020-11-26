### 题目描述
给定两个数组，编写一个函数来计算它们的交集。

### 示例
**示例 1：**
```
输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2,2]
```
**示例 2：**
```
输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[4,9]
```

**说明：**

- 输出结果中每个元素出现的次数，应与元素在两个数组中出现次数的最小值一致。
- 我们可以不考虑输出结果的顺序。

**进阶：**

- 如果给定的数组已经排好序呢？你将如何优化你的算法？
- 如果 `nums1` 的大小比 `nums2` 小很多，哪种方法更优？
- 如果 `nums2` 的元素存储在磁盘上，内存是有限的，并且你不能一次加载所有的元素到内存中，你该怎么办？

### 题解
#### 题解一
给数组做一组标志位数组
```
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        long start = System.currentTimeMillis();
		int len1=nums1.length;
		int len2=nums2.length;
		boolean[] bl=new boolean[len2];
		ArrayList<Integer> al=new ArrayList<Integer>();
		for(int i=0;i<len1;i++) {
			for(int j=0;j<len2;j++) {
				if(nums1[i]==nums2[j] && bl[j]==false) {
					al.add(nums1[i]);
					bl[j]=true;
					break;
				}
			}
		}
		int[] in = new int[al.size()];
		int e=0;
		for(int i:al)
			in[e++] = i;
		
		long end = System.currentTimeMillis();
		System.out.println(end-start);
		return in;
    }
}
```

####题解二
使用Map，数组作为键值key，计数器作为value

```
public int[] intersect2(int[] nums1, int[] nums2) {
	Map<Integer,Integer> map = new HashMap<Integer,Integer>();
	for(int i=0;i<nums1.length;i++) {
		Integer val=map.get(nums1[i]);
		map.put(nums1[i], (val==null)?1:++val);
	}
	ArrayList<Integer> al = new ArrayList<Integer>();
	for(int i=0,val;i<nums2.length;i++) {
		if(map.containsKey(nums2[i]) && (val=map.get(nums2[i]))>0) {
			al.add(nums2[i]);
			map.put(nums2[i], --val);
		}
	}
	
	int[] in = new int[al.size()];
	int e=0;
	for(int i:al)
		in[e++] = i;
	return in;
	
}
```

####题解三
排好序后比较移动指针
```
public static int[] intersect3(int[] nums1, int[] nums2) {
	Arrays.sort(nums1);
	Arrays.sort(nums2);
	int len1=nums1.length;
	int len2=nums2.length;
	ArrayList<Integer> al=new ArrayList<Integer>();
	for(int i=0,j=0;i<len1 && j<len2;) {
		if(nums1[i] == nums2[j]) {
			al.add(nums1[i]);
			i++;
			j++;
		}
		else if(nums1[i] > nums2[j]) {
			j++;
		}
		else {
			i++;
		}	
	}

	int[] in = new int[al.size()];
	int e=0;
	for(int i:al)
		in[e++] = i;
	return in;
}
```