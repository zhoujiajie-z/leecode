# 数组

## 简单题

### 1. 两数之和

> 给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出和为目标值 target 的那两个整数，并返回它们的数组下标。
>
> 你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。
>
> 你可以按任意顺序返回答案。

示例1：

```java
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
```

示例2：

```java
输入：nums = [3,2,4], target = 6
输出：[1,2]
```

示例3：

```java
输入：nums = [3,3], target = 6
输出：[0,1]
```

代码：

- 废物版

```java
import java.util.Scanner;

public class TwoSum {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] nums= new int[n];
        for (int i = 0; i < nums.length; i++) {
            nums[i] = sc.nextInt();
        }
        System.out.println(nums);
        System.out.println("请输入target：");
        int target = sc.nextInt();

        int aim[] = twoSum(nums, target);
        for (int i = 0; i < aim.length; i++) {
            if(i == 0){
                System.out.print("[");
            }

            System.out.print(aim[i]);

            if(i != aim.length - 1){
                System.out.print(",");
            }

            if(i == aim.length - 1){
                System.out.println("]");
            }
        }
    }

    public static int[] twoSum(int[] sums, int target){
        int[] aim = new int[2];
        for (int i = 0; i < sums.length; i++) {
            for (int j = i + 1; j < sums.length; j++) {
                if(sums[i] + sums[j] == target){
                    aim[0] = i;
                    aim[1] = j;
                    break;
                }
            }
        }
        return aim;
    }
}
```

- 大佬标准答案版

```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] indexs = new int[2];
        
        // 建立k-v ，一一对应的哈希表
        HashMap<Integer,Integer> hash = new HashMap<Integer,Integer>();
        for(int i = 0; i < nums.length; i++){
            if(hash.containsKey(nums[i])){
                indexs[0] = i;
                indexs[1] = hash.get(nums[i]);
                return indexs;
            }
            // 将数据存入 key为补数 ，value为下标
            hash.put(target-nums[i],i);
        }
        return indexs;
    }
}
```

### 26.删除有序数组中的重复项

> 给你一个有序数组 nums ，请你原地删除重复出现的元素，使每个元素只出现一次 ，返回删除后数组的新长度。
>
> 不要使用额外的数组空间，你必须在原地修改输入数组 并在使用 O(1) 额外空间的条件下完成。

示例1：

```java
输入：nums = [1,1,2]
输出：2, nums = [1,2]
解释：函数应该返回新的长度 2 ，并且原数组 nums 的前两个元素被修改为 1, 2 。不需要考虑数组中超出新长度后面的元素。
```

示例2：

```java
输入：nums = [0,0,1,1,1,2,2,3,3,4]
输出：5, nums = [0,1,2,3,4]
解释：函数应该返回新的长度 5 ， 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4 。不需要考虑数组中超出新长度后面的元素。
```

代码：

* 废物版

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if(nums.length < 2){	//如果数组只有一个元素 则直接返回数组长度 不存在重复元素
            return nums.length;
        }
        int j = 0;
        for(int i = 0; i< nums.length - 1;i++){
            if(nums[i] != nums[i+1]){	//如果元素与后一个元素不同
                nums[++j] = nums[i+1];	//令nums[j+1] = nums[i+1]
            }
        }
        return j + 1;		//则j+1为数组长度
    }
}
```

* 大佬版

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if(nums == null || nums.length == 0) return 0;
        int p = 0;
        int q = 1;
        while(q < nums.length){
            if(nums[p] != nums[q]){
                nums[p + 1] = nums[q];
                p++;
            }
            q++;
        }
        return p + 1;
    }
}
```

### 27.移除元素

> 给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素，并返回移除后数组的新长度。
>
> 不要使用额外的数组空间，你必须仅使用 O(1) 额外空间并 原地 修改输入数组。
>
> 元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。
>

示例1：

```java
输入：nums = [3,2,2,3], val = 3
输出：2, nums = [2,2]
解释：函数应该返回新的长度 2, 并且 nums 中的前两个元素均为 2。你不需要考虑数组中超出新长度后面的元素。例如，函数返回的新长度为 2 ，而 nums = [2,2,3,3] 或 nums = [2,2,0,0]，也会被视作正确答案。
```

示例2：

```java
输入：nums = [0,1,2,2,3,0,4,2], val = 2
输出：5, nums = [0,1,4,0,3]
解释：函数应该返回新的长度 5, 并且 nums 中的前五个元素为 0, 1, 3, 0, 4。注意这五个元素可为任意顺序。你不需要考虑数组中超出新长度后面的元素。
```

代码：

* 废物版

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int j = 0;
        for(int i = 0;i < nums.length;i++){
            if(nums[i] != val){
                nums[j++] = nums[i];
            }
        }
        return j;
    }
}
```

* 大佬版

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int left = 0;
        int right = nums.length;
        while (left < right) {
            if (nums[left] == val) {
                nums[left] = nums[right - 1];
                right--;
            } else {
                left++;
            }
        }
        return left;
    }
}
```

### 35.搜索插入的位置

> 给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。
>
> 请必须使用时间复杂度为 O(log n) 的算法。

示例1：

```java
输入: nums = [1,3,5,6], target = 5
输出: 2
```

示例2：

```java
输入: nums = [1,3,5,6], target = 2
输出: 1
```

示例3：

```java
输入: nums = [1,3,5,6], target = 7
输出: 4
```

示例4：

```java
输入: nums = [1,3,5,6], target = 0
输出: 0
```

示例5：

```java
输入: nums = [1], target = 0
输出: 0
```

代码：

* 废物版

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int j = 0;
        for(int i = 0; i < nums.length; i++){
            if(nums[i] == target){
                j = i;
                break;
            }else if(target < nums[0]){
                j = 0;
                break;
            }else if(target > nums[nums.length - 1]){
                j = nums.length;
                break;
            }else if(target > nums[i] && target < nums[i + 1]){
                j = i + 1;
                break;
            }
        }
        return j;
    }
}
```

* 大佬版

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        while(left <= right) {
            int mid = (left + right) / 2;
            if(nums[mid] == target) {
                return mid;
            } else if(nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return left;
    }
}
```





## 中等题



## 困难题

