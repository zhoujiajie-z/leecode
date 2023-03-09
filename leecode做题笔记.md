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
//暴力p
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
//二分搜索
public int searchInsert(int[] nums, int target) {
    int left = 0;
    int right = nums.length - 1;
    while(left <= right){
        int mid = (right - left) / 2 + left;
        if(nums[mid] == target){
            return mid;
        }else if(nums[mid] > target){
            right = mid - 1;
        }else {
            left = mid + 1;
        }
    }
    return left;
}
//二分搜索：数组方法调用
public int searchInsert(int[] nums, int target) {
    int search = Arrays.binarySearch(nums,target);
    if(search >= 0){
        return search;
    }else {
        return -search -1;
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

### 53.最大子数组和

>给你一个整数数组 `nums` ，请你找出一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。
>
>**子数组** 是数组中的一个连续部分。

示例1：

```java
输入：nums = [-2,1,-3,4,-1,2,1,-5,4]
输出：6
解释：连续子数组 [4,-1,2,1] 的和最大，为 6 。
```

示例2：

```java
输入：nums = [1]
输出：1
```

示例3：

```java
输入：nums = [5,4,-1,7,8]
输出：23
```

代码：

* 废物版

```java
// 动态规划解决问题
class Solution {
    public int maxSubArray(int[] nums) {
        int pre = 0;
        int maxPre = nums[0];
        int max = nums[0];
        for(int i = 1;i < nums.length; i++){
            pre = nums[i-1];
            if(pre >= 0){
                nums[i] = nums[i] + pre;
            }
            maxPre = Math.max(pre,maxPre);
            max = Math.max(nums[i],maxPre);
        }
        return max;
    }
}
```

* 大佬版

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int pre = 0, maxAns = nums[0];
        for (int x : nums) {
            pre = Math.max(pre + x, x);
            maxAns = Math.max(maxAns, pre);
        }
        return maxAns;
    }
}
```

### 66.加一

> 给定一个由 整数 组成的 非空 数组所表示的非负整数，在该数的基础上加一。最高位数字存放在数组的首位， 数组中每个元素只存储单个数字。你可以假设除了整数 0 之外，这个整数不会以零开头

示例1：

```java
输入：digits = [1,2,3]
输出：[1,2,4]
解释：输入数组表示数字 123
```

示例2：

```java
输入：digits = [4,3,2,1]
输出：[4,3,2,2]
解释：输入数组表示数字 4321
```

示例3：

```java
输入：digits = [0]
输出：[1]
```

代码

```java
class Solution {
    public int[] plusOne(int[] digits) {
        //从最后一位开始遍历数组
        for (int i = digits.length - 1; i >= 0; i--) {
            //如果最后一位为9，则进位后最后一位为0，继续遍历，直至不为9的那位加一
            if (digits[i] == 9) {
                digits[i] = 0;
            } else {
                //如果最后一位不为9，则直接加一后返回
                digits[i] += 1;
                return digits;
            }
        }
        //如果所有位均为9，则对数组扩容，数组位数+1，令数组首位为1，其余位默认为0
        digits = new int[digits.length + 1];
        digits[0] = 1;
        return digits;
    }
}
```

```java
//官方答案
class Solution {
    public int[] plusOne(int[] digits) {
        int n = digits.length;
        for (int i = n - 1; i >= 0; --i) {
            if (digits[i] != 9) {
                ++digits[i];
                for (int j = i + 1; j < n; ++j) {
                    digits[j] = 0;
                }
                return digits;
            }
        }

        // digits 中所有的元素均为 9
        int[] ans = new int[n + 1];
        ans[0] = 1;
        return ans;
    }
}
```

### 88. 合并两个有序数组

> 给你两个按 非递减顺序 排列的整数数组 nums1 和 nums2，另有两个整数 m 和 n ，分别表示 nums1 和 nums2 中的元素数目。请你 合并 nums2 到 nums1 中，使合并后的数组同样按 非递减顺序 排列。
>
> 注意：最终，合并后数组不应由函数返回，而是存储在数组 nums1 中。为了应对这种情况，nums1 的初始长度为 m + n，其中前 m 个元素表示应合并的元素，后 n 个元素为 0 ，应忽略。nums2 的长度为 n 。

示例1：

```java
输入：nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
输出：[1,2,2,3,5,6]
解释：需要合并 [1,2,3] 和 [2,5,6] 。
合并结果是 [1,2,2,3,5,6] ，其中斜体加粗标注的为 nums1 中的元素
```

示例2：

```java
输入：nums1 = [1], m = 1, nums2 = [], n = 0
输出：[1]
解释：需要合并 [1] 和 [] 。
合并结果是 [1] 
```

示例3：

```java
输入：nums1 = [0], m = 0, nums2 = [1], n = 1
输出：[1]
解释：需要合并的数组是 [] 和 [1] 。
合并结果是 [1] 。
注意，因为 m = 0 ，所以 nums1 中没有元素。nums1 中仅存的 0 仅仅是为了确保合并结果可以顺利存放到 nums1 中
```

代码：

> 思路
>
> 标签：从后向前数组遍历
>
> * 因为 nums1 的空间都集中在后面，所以从后向前处理排序的数据会更好，节省空间，一边遍历一边将值填充进去
> * 设置指针 len1 和 len2 分别指向 nums1 和 nums2 的有数字尾部，从尾部值开始比较遍历，同时设置指针 len 指向 nums1 的最末尾，每次遍历比较值大小之后，则进行填充
> * 当 len1<0 时遍历结束，此时 nums2 中海油数据未拷贝完全，将其直接拷贝到 nums1 的前面，最后得到结果数组
> * 时间复杂度：O(m+n)O(m+n)O(m+n)

```java
	public void merge(int[] nums1, int m, int[] nums2, int n) {
        int len1 = m - 1;
        int len2 = n - 1;
        int len = m + n - 1;
        while (len1 >= 0 && len2 >= 0) {
            nums1[len--] = nums1[len1] > nums2[len2] ? nums1[len1--] : nums2[len2--];
        }
        System.arraycopy(nums2, 0, nums1, 0, len2 + 1);
    }
```

> arraycopy（System类的静态方法）:
>
> public static void arraycopy(Object src, int srcPos, Object dest, int destPos, int length)
> src - 源数组。
> srcPos - 源数组中的起始位置。
> dest - 目标数组。
> destPos - 目标数据中的起始位置
> length - 要复制的数组元素的数量

### 108. 将有序数组转换为二叉搜索树

> 给你一个整数数组 nums ，其中元素已经按 升序 排列，请你将其转换为一棵 高度平衡 二叉搜索树。
> 高度平衡 二叉树是一棵满足「每个节点的左右两个子树的高度差的绝对值不超过 1 」的二叉树。
> `nums` 按 **严格递增** 顺序排列

示例一：

```java
输入：nums = [-10,-3,0,5,9]
输出：[0,-3,9,-10,null,5]
解释：[0,-10,5,null,-3,null,9] 也将被视为正确答案：
```

示例二：

```java
输入：nums = [1,3]
输出：[3,1]
解释：[1,null,3] 和 [3,1] 都是高度平衡二叉搜索树。
```

代码：

> 思路：
>
> nums按照严格递增顺序排列，则即为中序遍历，选取中间元素作为根节点，依次建立根节点的左右子树；

```java
public TreeNode sortedArrayToBST(int[] nums) {
     return helper(nums, 0, nums.length - 1);
}
 public TreeNode helper(int nums[],int left, int right){
     if(left>right){
         return null;
     }
     int mid = (left + right)/2;
     TreeNode treeNode = new TreeNode(nums[mid]);
     treeNode.left = helper(nums, left, mid - 1);
     treeNode.right = helper(nums, mid + 1, right);
     return treeNode;
}
```

### 118. 杨辉三角

> 给定一个非负整数 *`numRows`，*生成「杨辉三角」的前 *`numRows`* 行

示例一：

```java
输入: numRows = 5 
输出: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
```

示例二：

```java
输入: numRows = 1
输出: [[1]]
```

代码：

```java
public List<List<Integer>> generate(int numRows) {
    List<List<Integer>> result = new ArrayList<>();
    int[][] dp = new int[numRows][numRows];
    dp[0][0] = 1;
    List<Integer> row = new ArrayList<>();
    row.add(dp[0][0]);
    result.add(row);
    if(numRows == 1){
        return result;
    }
    for(int i = 1; i < numRows; i++){
        dp[i][0] = 1;
        dp[i][i] = 1;
        List<Integer> rows = new ArrayList<>();
        rows.add(dp[i][0]);
        for(int j = 1; j < i; j++){
            dp[i][j] = dp[i-1][j-1] + dp[i-1][j];
            rows.add(dp[i][j]);
        }
        rows.add(dp[i][i]);
        result.add(rows);
    }  
    return result;
}
```

### 119. 杨辉三角2

> 给定一个非负索引 `rowIndex`，返回「杨辉三角」的第 `rowIndex` 行

示例一：

```java
输入: rowIndex = 3 
输出: [1,3,3,1]
```

示例二：

```java
输入: rowIndex = 0 
输出: [1]
```

示例三：

```java
输入: rowIndex = 1 
输出: [1,1]
```

代码：

* 废物版

```java
public List<Integer> getRow(int rowIndex) {
    List<List<Integer>> result = new ArrayList<>();
    int[][] dp = new int[rowIndex + 1][rowIndex + 1];
    dp[0][0] = 1;
    List<Integer> row = new ArrayList<>();
    row.add(dp[0][0]);
    result.add(row);
    for (int i = 1; i <= rowIndex; i++) {
        List<Integer> rows = new ArrayList<>();
        dp[i][0] = 1;
        dp[i][i] = 1;
        rows.add(dp[i][0]);
        for (int j = 1; j < i; j++) {
            dp[i][j] = dp[i-1][j-1] + dp[i-1][j];
            rows.add(dp[i][j]);
        }
        rows.add(dp[i][i]);
        result.add(rows);
    }
    return result.get(rowIndex);
}
```

* 优化

```java
public List<Integer> getRow(int rowIndex) {
    List<Integer> row = new ArrayList<>();
    int[][] dp = new int[rowIndex + 1][rowIndex + 1];
    dp[0][0] = 1;
    row.add(dp[0][0]);
    for (int i = 1; i <= rowIndex; i++) {
        dp[i][0] = 1;
        dp[i][i] = 1;
        List<Integer> temp = new ArrayList<>();
        temp.add(dp[i][0]);
        for (int j = 1; j < i; j++) {
            dp[i][j] = dp[i-1][j-1]+dp[i-1][j];
            temp.add(dp[i][j]);
        }
        temp.add(dp[i][i]);
        row = temp;
    }
    return row;
}
```

官方答案：

```java
public List<Integer> getRow(int rowIndex) {
    List<List<Integer>> C = new ArrayList<List<Integer>>();
    for (int i = 0; i <= rowIndex; ++i) {
        List<Integer> row = new ArrayList<Integer>();
        for (int j = 0; j <= i; ++j) {
            if (j == 0 || j == i) {
                row.add(1);
            } else {
                row.add(C.get(i - 1).get(j - 1) + C.get(i - 1).get(j));
            }
        }
        C.add(row);
    }
    return C.get(rowIndex);
}
```

优化：

```java
public List<Integer> getRow(int rowIndex) {
    List<Integer> pre = new ArrayList<Integer>();
    for (int i = 0; i <= rowIndex; ++i) {
        List<Integer> cur = new ArrayList<Integer>();
        for (int j = 0; j <= i; ++j) {
            if (j == 0 || j == i) {
                cur.add(1);
            } else {
                cur.add(pre.get(j - 1) + pre.get(j));
            }
        }
        pre = cur;
    }
    return pre;
}
```

### 121. 买卖股票的最佳时机

> 给定一个数组 prices ，它的第 i 个元素 prices[i] 表示一支给定股票第 i 天的价格。
> 你只能选择某一天买入这只股票，并选择在未来的某一个不同的日子卖出该股票。设计一个算法来计算你所能获取的最大利润。
> 返回你可以从这笔交易中获取的最大利润。如果你不能获取任何利润，返回 0 。

示例一：

```java
输入：[7,1,5,3,6,4]
输出：5
解释：在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格；同时，你不能在买入前卖出股票。
```

示例二：

```java
输入：prices = [7,6,4,3,1]
输出：0
解释：在这种情况下, 没有交易完成, 所以最大利润为 0。
```

代码：

```java
public int maxProfit(int[] prices) {
    int length = prices.length;
    if (length < 2) {
        return 0;
    }
    int[] dp = new int[2];
    dp[0] = 0;
    dp[1] = -prices[0];
    for (int i = 1; i < length; i++) {
        //dp[0]:手中没有股票
        //dp[1]:z
        dp[0] = Math.max(dp[0], dp[1] + prices[i]);
        dp[1] = Math.max(dp[1], -prices[i]);
    }
    return dp[0];
}
```

```java
public int maxProfit(int[] prices) {
    int length = prices.length;
    if (length < 2) {
        return 0;
    }
    int[][] dp = new int[length][2];
    //dp[i][0]:第i天手中没有股票，两种情况：i-1天没有买入，i天也没有买入；i-1天有，i天卖出
    //dp[i][1]:第i天手中有股票，两种情况：i-1天手中有股票，i天也有；i-1天手中没有，i天买入
    dp[0][0] = 0;
    dp[0][1] = -prices[0];
    for (int i = 1; i < length; i++) {
        dp[i][0] = Math.max(dp[i-1][0], dp[i-1][1]+prices[i]);
        dp[i][1] = Math.max(dp[i-1][1], -prices[i]);
    }
    return dp[length-1][0];
}
```

官方答案：

```java
public int maxProfit(int[] prices) {
    //MAX_VALUE:表示int数据类型的最大取值数：2 147 483 647
    int minPrice = Integer.MAX_VALUE;
    int MaxProfit = 0;
    for (int i = 0; i < prices.length; i++) {
        if(minPrice > prices[i]){
            minPrice = prices[i];
        }else if(prices[i] - minPrice > MaxProfit){
            MaxProfit = prices[i] - minPrice;
        }
    }
    return MaxProfit;
}
```

### 136. 只出现一次的数字

> 给定一个**非空**整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

示例一：

```java
输入: [2,2,1]
输出: 1
```

示例二：

```java
输入: [4,1,2,1,2]
输出: 4
```

> 异或运算
>
> 一个数和 0 做 XOR 运算等于本身： a⊕0 = a
> 一个数和其本身做 XOR 运算等于 0： a⊕a = 0
> XOR 运算满足交换律和结合律： a⊕b⊕a = (a⊕a)⊕b = 0⊕b = b
>
> 题中信息是每个元素均出现两次，即可异或为0，再与唯一一个元素异或，得到的值就是出现一次的元素

代码：

```java
public int singleNumber(int[] nums) {
    int single = 0;
    for (int i : nums) {
        single = single ^ i;
    }
    return single;
}
```

### 169. 多数元素

>  给定一个大小为 *n* 的数组，找到其中的多数元素。多数元素是指在数组中出现次数 **大于** `⌊ n/2 ⌋` 的元素。你可以假设数组是非空的，并且给定的数组总是存在多数元素。

示例一：

```java
输入：[3,2,3] 
输出：3
```

示例二：

```java
输入：[2,2,1,1,1,2,2]
输出：2
```

代码：

```java
//废物版
public int majorityElement(int[] nums) {
    int result = 0;
    for (int i = 0; i < nums.length; i++) {
        int count = 0;
        for (int j = i; j < nums.length; j++) {
            if(nums[i] == nums[j]){
                count++;
            }
        }
        if(count > nums.length /2){
            result = nums[i];
        }
    }
    return result;
}
//官方答案:HashMap
// 使用哈希映射（HashMap）来存储每个元素以及出现的次数。对于哈希映射中的每个键值对，键表示一个元素，值表示该元素出现的次数。
// 用一个循环遍历数组 nums 并将数组中的每个元素加入哈希映射中。在这之后，我们遍历哈希映射中的所有键值对，返回值最大的键。我们同样也可以在遍历数组 nums 时候使用打擂台的方法，维护最大的值，这样省去了最后对哈希映射的遍历
public int majorityElement(int[] nums) {
    Map<Integer, Integer> counts = countNum(nums);
    Map.Entry<Integer, Integer> majorityEntry = null;
    for (Map.Entry<Integer, Integer> entry :
         counts.entrySet()) {
        if(majorityEntry == null || entry.getValue() > majorityEntry.getValue()){
            majorityEntry = entry;
        }
    }
    return majorityEntry.getKey();
}
public Map<Integer, Integer> countNum(int[] nums){
    Map<Integer, Integer> counts = new HashMap<Integer, Integer>();
    for (int num : nums) {
        if (!counts.containsKey(num)) {
            counts.put(num, 1);
        }else{
            counts.put(num, counts.get(num) + 1);
        }
    }
    return counts;
}
//排序算法
//如果将数组 nums 中的所有元素按照单调递增或单调递减的顺序排序，那么下标为n/2（下标从 0 开始）一定是众数。
public int majorityElement(int[] nums) {
    Arrays.sort(nums);
    return nums[nums.length/2];
}
//分治算法
//我们使用经典的分治算法递归求解，直到所有的子问题都是长度为 1 的数组。长度为 1 的子数组中唯一的数显然是众数，直接返回即可。如果回溯后某区间的长度大于 1，我们必须将左右子区间的值合并。如果它们的众数相同，那么显然这一段区间的众数是它们相同的值。否则，我们需要比较两个众数在整个区间内出现的次数来决定该区间的众数。

public int majorityElement(int[] nums) {
    return majorityElementRec(nums,0, nums.length - 1);
}

public int countInRange(int[] nums, int num, int left, int right) {
    int count = 0;
    for (int i = left; i <= right; i++) {
        if (nums[i] == num) {
            count++;
        }
    }
    return count;
}

public int majorityElementRec(int[] nums, int left, int right) {
    if (left == right) {
        return nums[left];
    }
    int mid = (left + right) / 2;
    int leftValue = majorityElementRec(nums, left, mid);
    int rightValue = majorityElementRec(nums, mid + 1, right);
    if (left == right) {
        return left;
    }
    int leftCount = countInRange(nums, leftValue, left, right);
    int rightCount = countInRange(nums, rightValue, left, right);
    return leftCount > rightCount ? leftValue : rightValue;
}
```

### 283. 移动零

> 给定一个数组 `nums`，编写一个函数将所有 `0` 移动到数组的末尾，同时保持非零元素的相对顺序。
>
> **请注意** ，必须在不复制数组的情况下原地对数组进行操作。

示例一：

```java
输入: nums = [0,1,0,3,12]
输出: [1,3,12,0,0]
```

示例二：

```java
输入: nums = [0]
输出: [0]
```

> 双指针方法思路：使用双指针，左指针指向当前已经处理好的序列的尾部，右指针指向待处理序列的头部。右指针不断向右移动，每次右指针指向非零数，则将左右指针对应的数交换，同时左指针右移。
>
> 注意到以下性质：
> 		左指针左边均为非零数；
> 		右指针左边直到左指针处均为零。

代码：

```java
//自己的方法，翻转数组
public void moveZeroes(int[] nums) {
    int end = nums.length -1;
    for (int i = 0; i <= end; i++) {
        if(nums[i] == 0){
            reverse(nums,i,end);
            end--;
            reverse(nums,i,end);
            i--;
        }
    }
}
public void reverse(int[] nums, int start, int end) {
    while (start < end) {
        int temp = nums[end];
        nums[end] = nums[start];
        nums[start] = temp;
        start++;
        end--;
    }
}
//双指针方法
public void moveZeroes(int[] nums) {
    int n = nums.length, left = 0, right = 0;
    while (right < n) {
        if (nums[right] != 0) {
            swap(nums, left, right);
            left++;
        }
        right++;
    }
}
public void swap(int[] nums, int left, int right) {
    int temp = nums[right];
    nums[right] = nums[left];
    nums[left] = temp;
}
```

### 661. 图片平滑器

> 图像平滑器 是大小为 3 x 3 的过滤器，用于对图像的每个单元格平滑处理，平滑处理后单元格的值为该单元格的平均灰度。
>
> 每个单元格的  平均灰度 定义为：该单元格自身及其周围的 8 个单元格的平均值，结果需向下取整。（即，需要计算蓝色平滑器中 9 个单元格的平均值）。
>
> 如果一个单元格周围存在单元格缺失的情况，则计算平均灰度时不考虑缺失的单元格（即，需要计算红色平滑器中 4 个单元格的平均值）。

示例一：

```java
输入:img = [[1,1,1],[1,0,1],[1,1,1]]
输出:[[0, 0, 0],[0, 0, 0], [0, 0, 0]]
解释:
对于点 (0,0), (0,2), (2,0), (2,2): 平均(3/4) = 平均(0.75) = 0
对于点 (0,1), (1,0), (1,2), (2,1): 平均(5/6) = 平均(0.83333333) = 0
对于点 (1,1): 平均(8/9) = 平均(0.88888889) = 0
```

示例二：

```java
输入: img = [[100,200,100],[200,50,200],[100,200,100]]
输出: [[137,141,137],[141,138,141],[137,141,137]]
解释:
对于点 (0,0), (0,2), (2,0), (2,2): floor((100+200+200+50)/4) = floor(137.5) = 137
对于点 (0,1), (1,0), (1,2), (2,1): floor((200+200+50+200+100+100)/6) = floor(141.666667) = 141
对于点 (1,1): floor((50+200+200+200+200+100+100+100+100)/9) = floor(138.888889) = 138
```

代码：

```java
public int[][] imageSmoother(int[][] img) {
    int m = img.length, n = img[0].length;
    int[][] ret = new int[m][n];
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            int num = 0, sum = 0;
            for (int x = i - 1; x <= i + 1; x++) {
                for (int y = j - 1; y <= j + 1; y++) {
                    if (x >= 0 && x < m && y >= 0 && y < n) {
                        num++;
                        sum += img[x][y];
                    }
                }
            }
            ret[i][j] = sum / num;
        }
    }
    return ret;
}
```

### 682. 棒球比赛

> 你现在是一场采用特殊赛制棒球比赛的记录员。这场比赛由若干回合组成，过去几回合的得分可能会影响以后几回合的得分。
>
> 比赛开始时，记录是空白的。你会得到一个记录操作的字符串列表 ops，其中 ops[i] 是你需要记录的第 i 项操作，ops 遵循下述规则：
>
>     整数 x - 表示本回合新获得分数 x
>     "+" - 表示本回合新获得的得分是前两次得分的总和。题目数据保证记录此操作时前面总是存在两个有效的分数。
>     "D" - 表示本回合新获得的得分是前一次得分的两倍。题目数据保证记录此操作时前面总是存在一个有效的分数。
>     "C" - 表示前一次得分无效，将其从记录中移除。题目数据保证记录此操作时前面总是存在一个有效的分数。
>
> 请你返回记录中所有得分的总和

示例一：

```java
输入：ops = ["5","2","C","D","+"]
输出：30
解释：
"5" - 记录加 5 ，记录现在是 [5]
"2" - 记录加 2 ，记录现在是 [5, 2]
"C" - 使前一次得分的记录无效并将其移除，记录现在是 [5].
"D" - 记录加 2 * 5 = 10 ，记录现在是 [5, 10].
"+" - 记录加 5 + 10 = 15 ，记录现在是 [5, 10, 15].
所有得分的总和 5 + 10 + 15 = 30
```

示例二：

```java
输入：ops = ["5","-2","4","C","D","9","+","+"]
输出：27
解释：
"5" - 记录加 5 ，记录现在是 [5]
"-2" - 记录加 -2 ，记录现在是 [5, -2]
"4" - 记录加 4 ，记录现在是 [5, -2, 4]
"C" - 使前一次得分的记录无效并将其移除，记录现在是 [5, -2]
"D" - 记录加 2 * -2 = -4 ，记录现在是 [5, -2, -4]
"9" - 记录加 9 ，记录现在是 [5, -2, -4, 9]
"+" - 记录加 -4 + 9 = 5 ，记录现在是 [5, -2, -4, 9, 5]
"+" - 记录加 9 + 5 = 14 ，记录现在是 [5, -2, -4, 9, 5, 14]
所有得分的总和 5 + -2 + -4 + 9 + 5 + 14 = 27
```

示例三：

```java
输入：ops = ["1"]
输出：1
```

代码：

```java
public int calPoints(String[] ops) {
    List<Integer> list = new ArrayList<Integer>();
    int n = -1;
    for(int i = 0;i < ops.length; i++){
        switch (ops[i]){
            case "+":
                list.add(list.get(n)+list.get(n-1));
                n++;
                break;
            case "D":
                list.add(list.get(n) * 2);
                n++;
                break;
            case "C":
                list.remove(n);
                n--;
                break;
            default:
                list.add(Integer.parseInt(ops[i]));
                n++;
        }
    }
    int result = 0;
    for(int i = 0; i < list.size(); i++){
        result += list.get(i);
    }
    return result;
}
//官方答案
public int calPoints(String[] ops) {
    int ret = 0;
    List<Integer> points = new ArrayList<Integer>();
    for (String op : ops) {
        int n = points.size();
        switch (op.charAt(0)) {
            case '+':
                ret += points.get(n - 1) + points.get(n - 2);
                points.add(points.get(n - 1) + points.get(n - 2));
                break;
            case 'D':
                ret += 2 * points.get(n - 1);
                points.add(2 * points.get(n - 1));
                break;
            case 'C':
                ret -= points.get(n - 1);
                points.remove(n - 1);
                break;
            default:
                ret += Integer.parseInt(op);
                points.add(Integer.parseInt(op));
                break;
        }
    }
    return ret;
}
```



### 704. 二分查找

> 给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target  ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。

示例一：

```java
输入: nums = [-1,0,3,5,9,12], target = 9
输出: 4
解释: 9 出现在 nums 中并且下标为 4
```

示例二：

```java
输入: nums = [-1,0,3,5,9,12], target = 2
输出: -1
解释: 2 不存在 nums 中因此返回 -1
```

代码：

> 二分查找的做法是，定义查找的范围 [left,right]，初始查找范围是整个数组。每次取查找范围的中点 mid，比较 nums[mid]和 target 的大小，如果相等则 mid即为要寻找的下标，如果不相等则根据 nums[mid]和 target的大小关系将查找范围缩小一半。
>
> 由于每次查找都会将查找范围缩小一半，因此二分查找的时间复杂度是 O(log⁡n)，其中 n 是数组的长度。
>
> 二分查找的条件是查找范围不为空，即 left≤right。如果 target在数组中，二分查找可以保证找到 target，返回 target在数组中的下标。如果 target 不在数组中，则当 left>right 时结束查找，返回 −1。
>

```java
//暴力搜索
public int search(int[] nums, int target) {
    for (int i = 0; i < nums.length; i++) {
        if(nums[i] == target){
            return i;
        }
    }
    return -1;
}
//二分查找：运用Arrays的方法
public int search(int[] nums, int target) {
    if(Arrays.binarySearch(nums,target) >= 0){
        return Arrays.binarySearch(nums,target);
    }
    return -1;
}
//二分查找：当left > right,表明查询结束，此时没查找到即为没有，跳出循环，返回-1
public int search(int[] nums, int target) {
    int left = 0;
    int right = nums.length - 1;
    while(left <= right){
        int mid = (left + right) / 2;
        if(nums[mid] == target){
            return mid;
        }else if(nums[mid] < target){
            left = mid + 1;
        }else if(nums[mid] > target){
            right = mid - 1;
        }
    }
    return -1;
}
```

### 733. 图像渲染

> 有一幅以 m x n 的二维整数数组表示的图画 image ，其中 image[i][j] 表示该图画的像素值大小。
>
> 你也被给予三个整数 sr ,  sc 和 newColor 。你应该从像素 image[sr][sc] 开始对图像进行 上色填充 。
>
> 为了完成 上色工作 ，从初始像素开始，记录初始坐标的 上下左右四个方向上 像素值与初始坐标相同的相连像素点，接着再记录这四个方向上符合条件的像素点与他们对应 四个方向上 像素值与初始坐标相同的相连像素点，……，重复该过程。将所有有记录的像素点的颜色值改为 newColor 。
>
> 最后返回 经过上色渲染后的图像 。

示例一：

```java
输入: image = [[1,1,1],[1,1,0],[1,0,1]]，sr = 1, sc = 1, newColor = 2
输出: [[2,2,2],[2,2,0],[2,0,1]]
解析: 在图像的正中间，(坐标(sr,sc)=(1,1)),在路径上所有符合条件的像素点的颜色都被更改成2。
注意，右下角的像素没有更改为2，因为它不是在上下左右四个方向上与初始点相连的像素点。
```

示例二：

```java
输入: image = [[0,0,0],[0,0,0]], sr = 0, sc = 0, newColor = 2
输出: [[2,2,2],[2,2,2]]
```

代码：

```java
public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
    return dfs(image,sr,sc,newColor,image[sr][sc]);
}
public int[][] dfs(int[][] image, int sr, int sc, int newColor, int num){
    if(sr<0||sr>=image.length||sc<0||sc>=image[0].length||newColor==image[sr][sc]||
image[sr][sc]!=num){
        return image;
    }else{
        int temp = image[sr][sc];
        image[sr][sc] = newColor;
        dfs(image,sr+1,sc,newColor,temp);
        dfs(image,sr-1,sc,newColor,temp);
        dfs(image,sr,sc+1,newColor,temp);
        dfs(image,sr,sc-1,newColor,temp);
    }
    return image;
} 
```

### 744. 寻找比目标字母大的最小字母

> 给你一个排序后的字符列表 letters ，列表中只包含小写英文字母。另给出一个目标字母 target，请你寻找在这一有序列表里比目标字母大的最小字母。
>
> 在比较时，字母是依序循环出现的。举个例子：
>
> 如果目标字母 target = 'z' 并且字符列表为 letters = ['a', 'b']，则答案返回 'a'

示例一：

```java
输入: letters = ["c", "f", "j"]，target = "a"
输出: "c"
```

示例二：

```java
输入: letters = ["c","f","j"], target = "c"
输出: "f"
```

示例三：

```java
输入: letters = ["c","f","j"], target = "d"
输出: "f"
```

思路：

> 利用列表有序的特点，可以使用二分查找降低时间复杂度。
>
> 首先比较目标字母和列表中的最后一个字母，当目标字母大于或等于列表中的最后一个字母时，答案是列表的首个字母。当目标字母小于列表中的最后一个字母时，列表中一定存在比目标字母大的字母，可以使用二分查找得到比目标字母大的最小字母。
>
> 初始时，二分查找的范围是整个列表的下标范围。每次比较当前下标处的字母和目标字母，如果当前下标处的字母大于目标字母，则在当前下标以及当前下标的左侧继续查找，否则在当前下标的右侧继续查找
>

代码：

```java
//暴力求解，直接用循环遍历，只要遇到第一个大于target的数，直接返回，如果一直没找到，则直接返回数组中的第一个元素
public char nextGreatestLetter(char[] letters, char target) {
    int len = letters.length;
    char result = letters[0];
    for(int i = 0; i < len; i++){
        if(letters[i] > target){
            result = letters[i];
            break;
        }
    }
    return result;
}
//二分法
public char nextGreatestLetter(char[] letters, char target) {
    int left = 0;
    int right = letters.length - 1;
    if(target >= letters[letters.length - 1]){
        return letters[0];
    }
    char min = letters[0];
    while(left < right){
        int mid = (right - left) / 2 + left;
        if(target < letters[mid]){
            right = mid;
        }else{
            left = mid + 1;
        }
    }
    return letters[left];
}
//官方答案
public char nextGreatestLetter(char[] letters, char target) {
    int length = letters.length;
    if (target >= letters[length - 1]) {
        return letters[0];
    }
    int low = 0, high = length - 1;
    while (low < high) {
        int mid = (high - low) / 2 + low;
        if (letters[mid] > target) {
            high = mid;
        } else {
            low = mid + 1;
        }
    }
    return letters[low];
}
```



### 977. 有序数组的平方

> 给你一个按 **非递减顺序** 排序的整数数组 `nums`，返回 **每个数字的平方** 组成的新数组，要求也按 **非递减顺序** 排序。

示例一：

```java
输入：nums = [-4,-1,0,3,10]
输出：[0,1,9,16,100]
解释：平方后，数组变为 [16,1,0,9,100]
排序后，数组变为 [0,1,9,16,100]
```

示例二：

```java
输入：nums = [-7,-3,2,3,11]
输出：[4,9,9,49,121]
```

> 双指针思路：如果数组 nums中的所有数都是非负数，那么将每个数平方后，数组仍然保持升序；如果数组 nums 中的所有数都是负数，那么将每个数平方后，数组会保持降序。
>
> 这样一来，如果我们能够找到数组 nums中负数与非负数的分界线，那么就可以用类似「归并排序」的方法了。具体地，我们设 neg 为数组 nums中负数与非负数的分界线，也就是说，nums[0]到 nums[neg]均为负数，而 nums[neg+1]到 nums[n−1]均为非负数。当我们将数组 nums 中的数平方后，那么 nums[0]到 nums[neg] 单调递减，nums[neg+1] 到 nums[n−1] 单调递增。
>
> 由于我们得到了两个已经有序的子数组，因此就可以使用归并的方法进行排序了。具体地，使用两个指针分别指向位置 neg 和 neg+1，每次比较两个指针对应的数，选择较小的那个放入答案并移动指针。当某一指针移至边界时，将另一指针还未遍历到的数依次放入答案。
>

代码：

```java
//直接排序：时间复杂度：O(nlogn)
public int[] sortedSquares(int[] nums) {
    int[] sqrtNums = new int[nums.length];
    for (int i = 0; i < nums.length; i++) {
        sqrtNums[i] = nums[i] * nums[i];
    }
    Arrays.sort(sqrtNums);
    return sqrtNums;
}
//双指针
public int[] sortedSquares(int[] nums) {
    int n = nums.length;
    int negative = -1;
    for (int i = 0; i < n; i++) {
        if (nums[i] < 0) {
            negative = i;
        } else {
            break;
        }
    }
    int i = negative，j = negative + 1，index = 0;
    int[] ans = new int[n];
    while (i >= 0 || j < n) {
        if (i < 0) {
            ans[index] = nums[j] * nums[j];
            j++;
        } else if (j == n) {
            ans[index] = nums[i] * nums[i];
            i--;
        } else if (nums[i] * nums[i] < nums[j] * nums[j]) {
            ans[index] = nums[i] * nums[i];
            i--;
        } else {
            ans[index] = nums[j] * nums[j];
            j++;
        }
        index++;
    }
    return ans;
}
//双指针：
public int[] sortedSquares(int[] nums) {
    int[] ans = new int[nums.length];
    for (int i = 0, j = nums.length - 1, pos = nums.length - 1; i <= j;) {
        if (nums[i] * nums[i] > nums[j] * nums[j]) {
            ans[pos] = nums[i] * nums[i];
            i++;
        } else {
            ans[pos] = nums[j] * nums[j];
            j--;
        }
        pos--;
    }
    return ans;
}
```



### [2562. 找出数组的串联值](https://leetcode.cn/problems/find-the-array-concatenation-value/)

> 给你一个下标从 0 开始的整数数组 nums 。
>
> 现定义两个数字的 串联 是由这两个数值串联起来形成的新数字。
>
> 例如，15 和 49 的串联是 1549 。
> nums 的 串联值 最初等于 0 。执行下述操作直到 nums 变为空：
>
> 如果 nums 中存在不止一个数字，分别选中 nums 中的第一个元素和最后一个元素，将二者串联得到的值加到 nums 的 串联值 上，然后从 nums 中删除第一个和最后一个元素。
> 如果仅存在一个元素，则将该元素的值加到 nums 的串联值上，然后删除这个元素。
> 返回执行完所有操作后 nums 的串联值。

示例一：

```java
输入：nums = [7,52,2,4]
输出：596
解释：在执行任一步操作前，nums 为 [7,52,2,4] ，串联值为 0 。
 - 在第一步操作中：
我们选中第一个元素 7 和最后一个元素 4 。
二者的串联是 74 ，将其加到串联值上，所以串联值等于 74 。
接着我们从 nums 中移除这两个元素，所以 nums 变为 [52,2] 。
 - 在第二步操作中： 
我们选中第一个元素 52 和最后一个元素 2 。 
二者的串联是 522 ，将其加到串联值上，所以串联值等于 596 。
接着我们从 nums 中移除这两个元素，所以 nums 变为空。
由于串联值等于 596 ，所以答案就是 596 。
```

示例二：

```java
输入：nums = [5,14,13,8,12]
输出：673
解释：在执行任一步操作前，nums 为 [5,14,13,8,12] ，串联值为 0 。 
- 在第一步操作中： 
我们选中第一个元素 5 和最后一个元素 12 。 
二者的串联是 512 ，将其加到串联值上，所以串联值等于 512 。 
接着我们从 nums 中移除这两个元素，所以 nums 变为 [14,13,8] 。
- 在第二步操作中：
我们选中第一个元素 14 和最后一个元素 8 。
二者的串联是 148 ，将其加到串联值上，所以串联值等于 660 。
接着我们从 nums 中移除这两个元素，所以 nums 变为 [13] 。 
- 在第三步操作中：
nums 只有一个元素，所以我们选中 13 并将其加到串联值上，所以串联值等于 673 。
接着我们从 nums 中移除这个元素，所以 nums 变为空。 
由于串联值等于 673 ，所以答案就是 673 。
```

代码：

```java
public long findTheArrayConcVal(int[] nums) {
  int left = 0, right = nums.length - 1;
  long res = 0;
  while(right > left){
    int tmp = Integer.valueOf(nums[left]+""+nums[right]);
    res += tmp;
    right--;
    left++;
  }
  if(left == right){
    res += nums[left];
  }
  return res;
}
```



## 中等题

### 11. 盛最多水的容器

> 给定一个长度为 n 的整数数组 height 。有 n 条垂线，第 i 条线的两个端点是 (i, 0) 和 (i, height[i]) 。
>
> 找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。
>
> 返回容器可以储存的最大水量。
>
> 说明：你不能倾斜容器。

示例一：

```java
输入：[1,8,6,2,5,4,8,3,7]
输出：49 
解释：图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。
```

示例二：

```java
输入：height = [1,1]
输出：1
```

代码：

```java
//O(N),O(1)
public int maxArea(int[] height) {
    int l = 0, r = height.length - 1;
    int ans = 0;
    while(l < r){
        int area = Math.min(height[l], height[r]) * (r - l);
        ans = Math.max(ans, area);
        if(height[l] < height[r]){
            l++;
        }else{
            r--;
        }
    }
    return ans;
}
```



### 15. 三数之和

> 给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有和为 0 且不重复的三元组。
>
> 注意：答案中不可以包含重复的三元组。

示例一：

```java
输入：nums = [-1,0,1,2,-1,-4]
输出：[[-1,-1,2],[-1,0,1]]
```

示例二：

```java
输入：nums = []
输出：[]
```

示例三：

```java
输入：nums = [0]
输出：[]
```

代码：

```java
//双指针：O(N^2),O(logn)
public List<List<Integer>> threeSum(int[] nums) {
    int n = nums.length;
    //先排序可以防止出现重复的三元组
    Arrays.sort(nums);
    List<List<Integer>> ans = new ArrayList<>();
    //枚举a
    for(int first = 0; first < n; first++){
        //要求与上次枚举的元素不同
        if(first > 0 && nums[first] == nums[first-1]){
            continue;
        }
        //指针c最初指向数组最右端
        int third = n - 1;
        int target = -nums[first];
        //枚举b
        for(int second = first + 1; second < n; second++){
            //要求与上次枚举的元素不同
            if(second > first + 1 && nums[second] == nums[second - 1]){
                continue;
            }
            //保证指针b在指针c的左侧
            while(second < third && nums[second] + nums[third] > target){
                third--;
            }
            //如果两个指针重合就可以退出循环
            if(second == third){
                break;
            }
            if(nums[second] + nums[third] == target){
                List<Integer> list = new ArrayList<>();
                list.add(nums[first]);
                list.add(nums[second]);
                list.add(nums[third]);
                ans.add(list);
            }
        }
    }
    return ans;
}
```

### [16. 最接近的三数之和](https://leetcode.cn/problems/3sum-closest/)

> 给你一个长度为 n 的整数数组 nums 和 一个目标值 target。请你从 nums 中选出三个整数，使它们的和与 target 最接近。
>
> 返回这三个数的和。
>
> 假定每组输入只存在恰好一个解。

示例一：

```java
输入：nums = [-1,2,1,-4], target = 1
输出：2
解释：与 target 最接近的和是 2 (-1 + 2 + 1 = 2) 。
```

示例二：

```java
输入：nums = [0,0,0], target = 1
输出：0
```

代码：

```java
//O(N^2), O(logN)
public int threeSumClosest(int[] nums, int target) {
  // 对数组进行排序防止重复枚举
  Arrays.sort(nums);
  int length = nums.length;
  int best = 1000000;
	// 枚举第一个数字
  for (int first = 0; first < length; first++) {
    // 保证和上一个枚举的元素不相等
    if (first > 0 && nums[first] == nums[first - 1]) {
      continue;
    }
    // 使用双指针枚举后两个数字
    int second = first + 1, third = length - 1;
    while (second < third) {
      int sum = nums[first] + nums[second] + nums[third];
      // 如果和为target则不可能存在比这个更接近的数字，直接返回
      if (sum == target) {
        return target;
      }
      // 根据差值的绝对值大小来更新答案
      if (Math.abs(sum - target) < Math.abs(best - target)) {
        best = sum;
      }
      // 如果和比target大，则令第三个数字左移
      if (sum > target) {
        int third_new = third - 1;
        // 移到下一个不相等的元素
        while (second < third_new && nums[third_new] == nums[third]) {
          third_new--;
        }
        third = third_new;
      } else {
        // 和比target小，第二个元素右移
        int second_new = second + 1;
        // 移到下一个不相等的元素
        while (second_new < third && nums[second_new] == nums[second]) {
          second_new++;
        }
        second = second_new;
      }
    }
  }
  return best;
}
```



### 33. 搜索旋转排序数组

> 整数数组 nums 按升序排列，数组中的值互不相同 。
>
> 在传递给函数之前，nums 在预先未知的某个下标 k（0 <= k < nums.length）上进行了旋转，使数组变为 [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]（下标 从 0 开始 计数）。例如， [0,1,2,4,5,6,7] 在下标 3 处经旋转后可能变为 [4,5,6,7,0,1,2] 。
>
> 给你旋转后的数组 nums 和一个整数 target ，如果 nums 中存在这个目标值 target ，则返回它的下标，否则返回 -1 。

示例一：

```java
输入：nums = [4,5,6,7,0,1,2], target = 0
输出：4
```

示例二：

```java
输入：nums = [4,5,6,7,0,1,2], target = 3
输出：-1
```

示例三：

```java
输入：nums = [1], target = 0
输出：-1
```

思路：

>对于有序数组，可以使用二分查找的方法查找元素。
>但是这道题中，数组本身不是有序的，进行旋转后只保证了数组的局部是有序的，这还能进行二分查找吗？答案是可以的。
>可以发现的是，我们将数组从中间分开成左右两部分的时候，一定有一部分的数组是有序的。拿示例来看，我们从 6 这个位置分开以后数组变成了 [4, 5, 6] 和 [7, 0, 1, 2] 两个部分，其中左边 [4, 5, 6] 这个部分的数组是有序的，其他也是如此。
>这启示我们可以在常规二分查找的时候查看当前 mid 为分割位置分割出来的两个部分 [l, mid] 和 [mid + 1, r] 哪个部分是有序的，并根据有序的那个部分确定我们该如何改变二分查找的上下界，因为我们能够根据有序的那部分判断出 target 在不在这个部分：
>如果 [l, mid - 1] 是有序数组，且 target 的大小满足 [nums[l],nums[mid])，则我们应该将搜索范围缩小至 [l, mid - 1]，否则在 [mid + 1, r] 中寻找。
>如果 [mid, r] 是有序数组，且 target 的大小满足 (nums[mid+1],nums[r]]，则我们应该将搜索范围缩小至 [mid + 1, r]，否则在 [l, mid - 1] 中寻找。
>
><img src="leecode%E5%81%9A%E9%A2%98%E7%AC%94%E8%AE%B0.assets/image-20220416152303514-16500937847202.png" alt="image-20220416152303514" style="zoom: 33%;" />
>
>需要注意的是，二分的写法有很多种，所以在判断 `target` 大小与有序部分的关系的时候可能会出现细节上的差别。

代码：

```java
//暴力解法：O(n)
public int search(int[] nums, int target) {
    for(int i = 0; i < nums.length; i++){
        if(nums[i] == target){
            return i;
        }
    }
    return -1;
}
//二分查找：O(logn)，O(1)
//将数组一分为二，其中一定有一个是有序的，另一个可能是有序，也能是部分有序。 此时有序部分用二分法查找。
//无序部分再一分为二，其中一个一定有序，另一个可能有序，可能无序。就这样循环.
public int search(int[] nums, int target) {
    int length = nums.length;
    if(length == 0){
        return -1;
    }
    if(length == 1){
        return nums[0] == target ? 0 : -1;
    }
    int left = 0, right = length - 1;
    while(left <= right){
        int mid = (right - left) / 2 + left;
        if(nums[mid] == target){
            return mid;
        }
        //mid左半边有序
        if(nums[0] <= nums[mid]){
            if(nums[0] <= target && target < nums[mid]){
                //target值在mid左侧
                right = mid - 1;
            }else{
                left = mid + 1;
            }
        }else{
            //mid右半边有序
            if(nums[mid] < target && target <= nums[length - 1]){
                //target值在mid右侧
                left = mid + 1;
            }else{
                right = mid - 1;
            }
        }
    }
    return -1;
}
```

### 34. 在排序数组中查找元素的第一个和最后一个位置

> 给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。
>
> 如果数组中不存在目标值 target，返回 [-1, -1]。
>
> 进阶：
>
> 你可以设计并实现时间复杂度为 O(log n) 的算法解决此问题吗？

示例一：

```java
输入：nums = [5,7,7,8,8,10], target = 8
输出：[3,4]
```

示例二：

```java
输入：nums = [5,7,7,8,8,10], target = 6
输出：[-1,-1]
```

示例三：

```java
输入：nums = [], target = 0
输出：[-1,-1]
```

思路：

> 直观的思路肯定是从前往后遍历一遍。用两个变量记录第一次和最后一次遇见 target的下标，但这个方法的时间复杂度为 O(n)，没有利用到数组升序排列的条件。
>
> 由于数组已经排序，因此整个数组是单调递增的，我们可以利用二分法来加速查找的过程。
>
> 考虑 target 开始和结束位置，其实我们要找的就是数组中「第一个等于 target的位置」（记为 leftIdx）和「第一个大于 target的位置减一」（记为 rightIdx）。
>
> 二分查找中，寻找 leftIdx即为在数组中寻找第一个大于等于 target 的下标，寻找 rightIdx即为在数组中寻找第一个大于 target的下标，然后将下标减一。两者的判断条件不同，为了代码的复用，我们定义 binarySearch(nums, target, lower) 表示在 nums 数组中二分查找 target的位置，如果 lower为 true，则查找第一个大于等于 target的下标，否则查找第一个大于 target的下标。
>
> 最后，因为 target可能不存在数组中，因此我们需要重新校验我们得到的两个下标 leftIdx和 rightIdx，看是否符合条件，如果符合条件就返回 [leftIdx,rightIdx]，不符合就返回 [−1,−1]。
>

代码：

```java
//暴力解法：O(n)
public int[] searchRange(int[] nums, int target) {
    boolean flag = true;
    int[] result = new int[2];
    for(int i = 0; i < nums.length; i++){
        if(flag && nums[i] == target){
            result[0] = i;
            flag = false;
        }
        if(!flag && nums[i] == target){
            result[1] = i;
        }
    }
    if(flag){
        return new int[]{-1,-1};
    }else{
        return result;
    }
}
//二分法: O(log⁡n),O(1)
public int[] searchRange(int[] nums, int target) {
    int start = binaarySearch(nums,target,true);
    int end = binaarySearch(nums,target,false) - 1;
    if(start <= end && end < nums.length && nums[start] == target && nums[end]== target){
        return new int[]{start,end};
    }
    return new int[]{-1,-1};
}

public int binaarySearch(int[] nums, int target, boolean lower){
    int left = 0, right = nums.length - 1, ans = nums.length;
    while(left <= right){
        int mid = (right - left) / 2 + left;
        //先找>=target的第一个
    	//再找>target的第一个
        if(nums[mid] > target || lower && nums[mid] >= target){
            right = mid - 1;
            ans = mid;
        }else{
            left = mid + 1;
        }
    }
    return ans;
}
```

### 74. 搜索二维矩阵

> 编写一个高效的算法来判断 m x n 矩阵中，是否存在一个目标值。该矩阵具有如下特性：
>
> 每行中的整数从左到右按升序排列。
> 每行的第一个整数大于前一行的最后一个整数。

示例一：

```java
输入：matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
输出：true
```

示例二：

```java
输入：matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
输出：false
```

思路：

> 方法一：两次二分查找
> 由于每行的第一个元素大于前一行的最后一个元素，且每行元素是升序的，所以每行的第一个元素大于前一行的第一个元素，因此矩阵第一列的元素是升序的。
> 我们可以对矩阵的第一列的元素二分查找，找到最后一个不大于目标值的元素，然后在该元素所在行中二分查找目标值是否存在。
>
> 方法二：一次二分查找
> 若将矩阵每一行拼接在上一行的末尾，则会得到一个升序数组，我们可以在该数组上二分找到目标元素。
> 代码实现时，可以二分升序数组的下标，将其映射到原矩阵的行和列上。

代码：

```java
//暴力解法：O(mn)，其中 mmm 和 nnn 分别是矩阵的行数和列数
public boolean searchMatrix(int[][] matrix, int target) {
    for(int i = 0; i < matrix.length; i++){
        for(int j = 0; j < matrix[0].length; j++){
            if(matrix[i][j] == target){
                return true;
            }
        }
    }
    return false;
}
//使用两次二分查找：O(logm + logn) = O(logmn),O(1)
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int row = binarySearch(matrix,target);
        if(row < 0 || row > matrix.length - 1){
            return false;
        }       
        return binarySearchRow(matrix[row],target);
    }
	//在0列进行二分查找，寻找target所在的行
    public int binarySearch(int[][] matrix, int target){
        int low = 0, high = matrix.length - 1, row = 0;
        while(low <= high){
            int mid = (high + low) / 2;
            if(matrix[mid][0] == target){
                return mid;
            }
            if(matrix[mid][0] > target){
                high = mid - 1;
            }else if(matrix[mid][0] < target){
                row = mid;
                low = mid + 1;
            }
        }
        return row;
    }
	//在row行进行二分查找
    public boolean binarySearchRow(int[] row, int target){
        int left = 0, right = row.length - 1;
        while(left <= right){
            int mid = (right - left) / 2 + left;
            if(row[mid] == target){
                return true;
            }
            if(row[mid] > target){
                right = mid -1;
            }else if(row[mid] < target){
                left = mid + 1;
            }
        }
        return false;
    }
}
//使用一次二分查找：O(logmn),O(1)
public boolean searchMatrix(int[][] matrix, int target) {
    int m = matrix.length, n = matrix[0].length;
    int left = 0, right = m * n - 1;
    while(left <= right){
        int mid = (right - left) / 2 + left;
        int x = matrix[mid / n][mid % n];
        if(x < target){
            left = mid + 1;
        }else if(x > target){
            right = mid - 1;
        }else{
            return true;
        }
    }
    return false;
}
```

### 153. 寻找旋转排序数组中的最小值

> 已知一个长度为 n 的数组，预先按照升序排列，经由 1 到 n 次 旋转 后，得到输入数组。例如，原数组 nums = [0,1,2,4,5,6,7] 在变化后可能得到：
>
> 若旋转 4 次，则可以得到 [4,5,6,7,0,1,2]
> 若旋转 7 次，则可以得到 [0,1,2,4,5,6,7]
>
> 注意，数组 [a[0], a[1], a[2], ..., a[n-1]] 旋转一次 的结果为数组 [a[n-1], a[0], a[1], a[2], ..., a[n-2]] 。
>
> 给你一个元素值 互不相同 的数组 nums ，它原来是一个升序排列的数组，并按上述情形进行了多次旋转。请你找出并返回数组中的 最小元素 。
>
> 你必须设计一个时间复杂度为 O(log n) 的算法解决此问题。

示例一：

```java
输入：nums = [3,4,5,1,2]
输出：1
解释：原数组为 [1,2,3,4,5] ，旋转 3 次得到输入数组。
```

示例二：

```java
输入：nums = [4,5,6,7,0,1,2]
输出：0
解释：原数组为 [0,1,2,4,5,6,7] ，旋转 4 次得到输入数组。
```

示例三：

```java
输入：nums = [11,13,15,17]
输出：11
解释：原数组为 [11,13,15,17] ，旋转 4 次得到输入数组。
```

思路：

>![image-20220418222550940](leecode%E5%81%9A%E9%A2%98%E7%AC%94%E8%AE%B0.assets/image-20220418222550940-16502919521302.png)
>
>![image-20220418222627526](leecode%E5%81%9A%E9%A2%98%E7%AC%94%E8%AE%B0.assets/image-20220418222627526-16502919892184.png)

代码：

```java
//暴力求解：O(n)
public int findMin(int[] nums) {
    int min = nums[0];
    for(int i = 1; i < nums.length; i++){
        if(min > nums[i]){
            min = nums[i];
        }
    }
    return min;
}
//二分查找：O(logn),O(1)
public int findMin(int[] nums) {
    int left = 0, right = nums.length - 1;
    while(left < right){
        int mid = (right - left) / 2 + left;
        if(nums[mid] > nums[right]){
            left = mid + 1;
        }else{
            right = mid;
        }
    }
    return nums[right];
}
```

### 162. 寻找峰值

> 峰值元素是指其值严格大于左右相邻值的元素。
>
> 给你一个整数数组 nums，找到峰值元素并返回其索引。数组可能包含多个峰值，在这种情况下，返回 任何一个峰值 所在位置即可。
>
> 你可以假设 nums[-1] = nums[n] = -∞ 。
>
> 你必须实现时间复杂度为 O(log n) 的算法来解决此问题。

示例一：

```java
输入：nums = [1,2,3,1]
输出：2
解释：3 是峰值元素，你的函数应该返回其索引 2。
```

示例二：

```java
输入：nums = [1,2,1,3,5,6,4]
输出：1 或 5 
解释：你的函数可以返回索引 1，其峰值元素为 2；
     或者返回索引 5， 其峰值元素为 6。
```

思路：

> **方法一：寻找最大值**
> 由于题目保证了 nums[i]≠nums[i+1]，那么数组 nums中最大值两侧的元素一定严格小于最大值本身。因此，最大值所在的位置就是一个可行的峰值位置。
> 我们对数组 nums进行一次遍历，找到最大值对应的位置即可。
>
> **方法二：迭代**
> 由于我们可以假设 nums[−1]=nums[n]=−∞，所以我们对于 i=0 需要特判，只要满足 nums[0]>nums[1]即可。同理，对于 i=n−1，只要有 nums[n−1]>nums[n−2]即可。
> 对于其余点，我们需要保证 nums[i]>nums[i+1]且 nums[i]>nums[i−1]
>
> **方法三：二分查找优化**
> 题目要求我们实现复杂度为 O(logn)的算法，又是数组中的搜索问题。所以我们自然而然想到尝试二分法。
> 在二分查找中，每次会找到一个位置 mid。我们发现，mid 只有如下三种情况：
> mid 为一个峰值，此时我们通过比较 mid 位置元素与两边元素大小即可。
> mid 在一个峰值右侧，此时有 nums[mid]<nums[mid+1]，此时我们向右调整搜索范围，在 [mid+1,r]范围内继续查找。
> mid 在一个峰值左侧，此时有 nums[mid]<nums[mid−1]，此时我们向左调整搜索范围，在 [l+1,mid]范围内继续查找。

代码：

```java
//暴力求解，直接查找数组中的最大值：O(n),O(1)
public int findPeakElement(int[] nums) {
    int max = 0;
    for(int i = 1; i < nums.length; i++){
        if(nums[max] < nums[i]){
            max = i;
        }
    }
    return max;
}
//迭代爬坡：O(n),O(1)
public int findPeakElement(int[] nums) {
    int n = nums.length;
    if(n == 1){
        return 0;
    }
    for(int i = 0; i < n; i++){
        if(i == 0){
            if(nums[i] > nums[i+1]){
                return i;
            }
        }else if(i == n - 1){
            if(nums[i] > nums[i-1]){
                return i;
            }
        }else{
            if(nums[i] > nums[i-1] && nums[i] > nums[i+1]){
                return i;
            }
        }
    }
    return -1;
}
//二分法：O(logn),O(1)
public int findPeakElement(int[] nums) {
    if(nums.length == 1){
        return 0;
    }
    if(nums[0] > nums[1]){
        return 0;
    }
    if(nums[nums.length - 1] > nums[nums.length - 2]){
        return nums.length - 1;
    }
    int left = 0, right = nums.length - 1;
    while(left <= right){
        int mid = (right - left) / 2 + left;
        if(mid >= 1 && mid <= nums.length - 2 && nums[mid] > nums[mid-1] && nums[mid] > nums[mid+1]){
            return mid;
        }else if(nums[mid] < nums[mid+1]){
            left = mid + 1;
        }else if(nums[mid] < nums[mid-1]){
            right = mid - 1;
        }
    }
    return -1;
}
```



### 167. 输入有序数组

> 给你一个下标从 1 开始的整数数组 numbers ，该数组已按 非递减顺序排列  ，请你从数组中找出满足相加之和等于目标数 target 的两个数。如果设这两个数分别是 numbers[index1] 和 numbers[index2] ，则
> 1 <= index1 < index2 <= numbers.length 。
> 以长度为 2 的整数数组 [index1, index2] 的形式返回这两个整数的下标 index1 和 index2。
> 你可以假设每个输入 只对应唯一的答案 ，而且你 不可以 重复使用相同的元素。
> 你所设计的解决方案必须只使用常量级的额外空间。

示例一：

```java
输入：numbers = [2,7,11,15], target = 9
输出：[1,2]
解释：2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。返回 [1, 2] 。
```

示例二：

```java
输入：numbers = [2,3,4], target = 6
输出：[1,3]
解释：2 与 4 之和等于目标数 6 。因此 index1 = 1, index2 = 3 。返回 [1, 3] 。
```

示例三：

```java
输入：numbers = [-1,0], target = -1
输出：[1,2]
解释：-1 与 0 之和等于目标数 -1 。因此 index1 = 1, index2 = 2 。返回 [1, 2] 。
```

> 思路：
>
> 1.二分查找：在数组中找到两个数，使得它们的和等于目标值，可以首先固定第一个数，然后寻找第二个数，第二个数等于目标值减去第一个数的差。利用数组的有序性质，可以通过二分查找的方法寻找第二个数。为了避免重复寻找，在寻找第二个数时，只在第一个数的右侧寻找
>
> 2.双指针：初始时两个指针分别指向第一个元素位置和最后一个元素的位置。每次计算两个指针指向的两个元素之和，并和目标值比较。如果两个元素之和等于目标值，则发现了唯一解。如果两个元素之和小于目标值，则将左侧指针右移一位。如果两个元素之和大于目标值，则将右侧指针左移一位。移动指针之后，重复上述操作，直到找到答案。

代码：

```java
//二分查找：O(nlogn)
public int[] twoSum(int[] numbers, int target) {
    int[] result = new int[2];
    for (int i = 0; i < numbers.length; i++) {
        int left = i + 1, right = numbers.length - 1;
        while(left <= right){
            int mid = (right - left) / 2 + left;
            if(numbers[mid] == target - numbers[i]){
                result[0] = i + 1;
                result[1] = mid + 1;
                break;
            }else if(numbers[mid] > target - numbers[i]){
                right = mid - 1;
            }else{
                left = mid + 1;
            }
        }
    }
    return result;
}
//双指针:O(n)
public int[] twoSum(int[] numbers, int target) {
    int[] result = new int[2];
    int left = 0, right = numbers.length - 1;
    while (left < right) {
        if (numbers[left] + numbers[right] == target) {
            result[0] = left + 1;
            result[1] = right + 1;
            break;
        } else if (numbers[left] + numbers[right] > target) {
            right -= 1;
        } else {
            left += 1;
        }
    }
    return result;
}
```

### 189. 轮转数组

> 给你一个数组，将数组中的元素向右轮转 `k` 个位置，其中 `k` 是非负数。

示例一：

```java
输入: nums = [1,2,3,4,5,6,7], k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右轮转 1 步: [7,1,2,3,4,5,6]
向右轮转 2 步: [6,7,1,2,3,4,5]
向右轮转 3 步: [5,6,7,1,2,3,4]
```

示例二：

```java
输入：nums = [-1,-100,3,99], k = 2
输出：[3,99,-1,-100]
解释: 
向右轮转 1 步: [99,-1,-100,3]
向右轮转 2 步: [3,99,-1,-100]
```

> 思路：
>
> 1. 使用额外的数组：我们可以使用额外的数组来将每个元素放至正确的位置。用 n 表示数组的长度，我们遍历原数组，将原数组下标为 iii 的元素放至新数组下标为 (i+k) mod n的位置，最后将新数组拷贝至原数组即可。
>
> 2. 翻转数组：该方法基于如下的事实：当我们将数组的元素向右移动 k 次后，尾部 k mod n个元素会移动至数组头部，其余元素向后移动 k mod n 个位置。
>
>    该方法为数组的翻转：我们可以先将所有元素翻转，这样尾部的 k mod n个元素就被移至数组头部，然后我们再翻转 [0,k mod n−1] 区间的元素和 [k mod n,n−1]区间的元素即能得到最后的答案。
>
> 3. 环状替换

代码：

```java
//使用额外数组：O(n)、O(n)
public void rotate(int[] nums, int k) {
    int n = nums.length;
    int[] newArr = new int[n];
    for (int i = 0; i < n; i++) {
        newArr[(i + k) % n] = nums[i];
    }
    System.arraycopy(newArr, 0, nums, 0, n);
}
//翻转数组：O(n)、O(1)
public void rotate(int[] nums, int k) {
    k = k % nums.length;
    reverse(nums, 0, nums.length - 1);
    reverse(nums, 0, k - 1);
    reverse(nums, k, nums.length - 1);
}
public void reverse(int[] nums, int start, int end) {
    while (start < end) {
        int temp = nums[end];
        nums[end] = nums[start];
        nums[start] = temp;
        start += 1;
        end -= 1;
    }
}
//环状替换：O(n)、O
public void rotate(int[] nums, int k) {
    int len = nums.length;
    k %= len;
    int count = 0;
    int start = 0;
    while (count < len) {
        int cur = start;
        int prev = nums[start];
        do {
            int next = (cur + k) % len;
            int temp = nums[next];
            nums[next] = prev;
            prev = temp;
            cur = next;
            count++;
        } while (cur != start);
        start++;
    }
}
```

### 380. O(1) 时间插入、删除和获取随机元素

> 实现RandomizedSet 类：
>
>     RandomizedSet() 初始化 RandomizedSet 对象
>     bool insert(int val) 当元素 val 不存在时，向集合中插入该项，并返回 true ；否则，返回 false 。
>     bool remove(int val) 当元素 val 存在时，从集合中移除该项，并返回 true ；否则，返回 false 。
>     int getRandom() 随机返回现有集合中的一项（测试用例保证调用此方法时集合中至少存在一个元素）。每个元素应该有 相同的概率 被返回。
>
> 你必须实现类的所有函数，并满足每个函数的 平均 时间复杂度为 O(1) .

示例：

```java
输入
["RandomizedSet", "insert", "remove", "insert", "getRandom", "remove", "insert", "getRandom"]
[[], [1], [2], [2], [], [1], [2], []]
输出
[null, true, false, true, 2, true, false, 2]

解释
RandomizedSet randomizedSet = new RandomizedSet();
randomizedSet.insert(1); // 向集合中插入 1 。返回 true 表示 1 被成功地插入。
randomizedSet.remove(2); // 返回 false ，表示集合中不存在 2 。
randomizedSet.insert(2); // 向集合中插入 2 。返回 true 。集合现在包含 [1,2] 。
randomizedSet.getRandom(); // getRandom 应随机返回 1 或 2 。
randomizedSet.remove(1); // 从集合中移除 1 ，返回 true 。集合现在包含 [2] 。
randomizedSet.insert(2); // 2 已在集合中，所以返回 false 。
randomizedSet.getRandom(); // 由于 2 是集合中唯一的数字，getRandom 总是返回 2 。
```

代码：

```java
class RandomizedSet {
    //存放元素val值
    List<Integer> nums;
    //存放元素val值和index值
    Map<Integer,Integer> indices;
    Random random;
    public RandomizedSet() {
        //初始化列表
        nums = new ArrayList<Integer>();
        indices = new HashMap<Integer,Integer>();
        random = new Random();
    }
    
    public boolean insert(int val) {
        //如果已经存在val值，则返回false
        if(indices.containsKey(val)){
            return false;
        }
        //确定索引值，即在列表中存放的位置
        int index = nums.size();
        nums.add(val);
        //将val放在key的位置是因为val的值不能重复
        indices.put(val,index);
        return true;
    }
    
    public boolean remove(int val) {
        //如果没有val元素则返回false
        if(!indices.containsKey(val)){
            return false;
        }
        //取val对应的索引值，即存放在列表中的位置
        int index = indices.get(val);
        //list列表中存放的最后一位对应的val值
        int last = nums.get(nums.size()-1);
        //用last值取代index位置的val值
        nums.set(index,last);
        //将最后一位的值取代原index位置的值，即替代
        indices.put(last,index);
        //将列表中最后一位val值删除，因为已经移到index位置上了，所以删除的还是传入的参数val值
        nums.remove(nums.size()-1);
        //将map中的val值删除
        indices.remove(val);
        return true;
    }
    
    public int getRandom() {
        //nextInt​(int bound)：返回伪随机的，均匀分布 int值介于0（含）和指定值（不包括），从该随机数生成器的序列绘制。
        //随机产生一位索引值
        int randomIndex = random.nextInt(nums.size());
        //f索引值对应的val值
        return nums.get(randomIndex);
    }
}
```

### 396. 旋转函数

> 给定一个长度为 n 的整数数组 nums 。
>
> 假设 arrk 是数组 nums 顺时针旋转 k 个位置后的数组，我们定义 nums 的 旋转函数  F 为：
>
>     F(k) = 0 * arrk[0] + 1 * arrk[1] + ... + (n - 1) * arrk[n - 1]
>
> 返回 F(0), F(1), ..., F(n-1)中的最大值 。
>
> 生成的测试用例让答案符合 32 位 整数。

示例一：

```java
输入: nums = [4,3,2,6]
输出: 26
解释:
F(0) = (0 * 4) + (1 * 3) + (2 * 2) + (3 * 6) = 0 + 3 + 4 + 18 = 25
F(1) = (0 * 6) + (1 * 4) + (2 * 3) + (3 * 2) = 0 + 4 + 6 + 6 = 16
F(2) = (0 * 2) + (1 * 6) + (2 * 4) + (3 * 3) = 0 + 6 + 8 + 9 = 23
F(3) = (0 * 3) + (1 * 2) + (2 * 6) + (3 * 4) = 0 + 2 + 12 + 12 = 26
所以 F(0), F(1), F(2), F(3) 中的最大值是 F(3) = 26 。
```

示例二：

```java
输入: nums = [100]
输出: 0
```

思路：

> ![image-20220423112844326](leecode%E5%81%9A%E9%A2%98%E7%AC%94%E8%AE%B0.assets/image-20220423112844326-16506845258841.png)
>
> ![image-20220423113900453](leecode%E5%81%9A%E9%A2%98%E7%AC%94%E8%AE%B0.assets/image-20220423113900453-16506851422922.png)

代码：

```java
//O(n),O(n)
public int maxRotateFunction(int[] nums) {
    int n = nums.length;
    int[] sum = new int[n*2+10];
    sum[0] = nums[0];
    for(int i = 1; i < 2*n; i++){
        sum[i] = sum[i-1] + nums[i % n];
    }
    int ans = 0;
    for(int i = 0; i < n; i++){
        ans += nums[i] * i;
    }
    for(int i = n, cur = ans; i < 2*n; i++){
        cur += nums[i % n] * (n -1);
        cur -= sum[i-1] - sum[i-n];
        ans = Math.max(ans, cur);
    }
    return ans;
}
//官方题解：O(n),O(1)
//理解版
public int maxRotateFunction(int[] nums) {
    int n = nums.length;
    int ans = 0;
    int sum = 0;
    int[] f = new int[n];
    for(int i = 0; i < n; i++){
        sum += nums[i];
    }
    for(int i = 0; i < n; i++){
        f[0] += nums[i] * i;
    }
    ans = f[0];
    for(int i = 1; i < n; i++){
        f[i] = f[i-1] + sum - n * nums[n-i];
        ans = Math.max(ans, f[i]);
    }
    return ans;
}
//答案版
public int maxRotateFunction(int[] nums) {
    int f = 0, n = nums.length, numSum = Arrays.stream(nums).sum();
    for (int i = 0; i < n; i++) {
        f += i * nums[i];
    }
    int res = f;
    for (int i = n - 1; i > 0; i--) {
        //不需要额外数组存放之前
        f += numSum - n * nums[i];
        res = Math.max(res, f);
    }
    return res;
}
```



### 542. 01矩阵

> 给定一个由 0 和 1 组成的矩阵 mat ，请输出一个大小相同的矩阵，其中每一个格子是 mat 中对应位置元素到最近的 0 的距离。
>
> 两个相邻元素间的距离为 1 。

示例一：

```java
输入：mat = [[0,0,0],[0,1,0],[0,0,0]]
输出：[[0,0,0],[0,1,0],[0,0,0]]
```

示例二：

```java
输入：mat = [[0,0,0],[0,1,0],[1,1,1]]
输出：[[0,0,0],[0,1,0],[1,2,1]]
```

代码：

```java
//广度优先搜索：O(ij),O(ij)
static int[][] dir = new int[][]{{1,0},{-1,0},{0,1},{0,-1}};	//方便移位运算
public int[][] updateMatrix(int[][] mat) {
    boolean[][] flag = new boolean[mat.length][mat[0].length];
    int[][] dist = new int[mat.length][mat[0].length];
    Queue<int[]> queue = new LinkedList<>();
    for(int i = 0; i < mat.length; i++){
        for(int j = 0; j < mat[0].length; j++){
            if(mat[i][j] == 0){
                queue.offer(new int[]{i,j});
                flag[i][j] = true;
            }
        }
    }
    while(!queue.isEmpty()){
        int[] cell = queue.poll();
        int i = cell[0], j = cell[1];
        for(int d = 0; d < 4; d++){
            int ni = i + dir[d][0];
            int nj = j + dir[d][1];
            while(ni >= 0 && ni < mat.length && nj >= 0 && nj < mat[0].length && !flag[ni][nj])			   {
                dist[ni][nj] = dist[i][j] + 1;
                queue.offer(new int[]{ni,nj});	//将新求的点的周围元也放入队尾
                flag[ni][nj] = true;
            }
        }
    }
    return dist;
}
//动态规划
public int[][] updateMatrix(int[][] mat) {
    int m = mat.length, n= mat[0].length;
    int[][] dist = new int[m][n];
    for(int i = 0; i < m; i++){
        Arrays.fill(dist[i], Integer.MAX_VALUE / 2);
    }
    //值为0，则距离为0
    for(int i = 0; i < m; i++){
        for(int j = 0; j < n; j++){
            if(mat[i][j] == 0){
                dist[i][j] = 0;
            }
        }
    }
    //坐标为0到1的距离
    //向右向下遍历
    for(int i =0; i < m; i++){
        for(int j = 0; j < n; j++){
            if(i - 1 >= 0){
                dist[i][j] = Math.min(dist[i][j], dist[i-1][j] + 1);
            }  
            if(j - 1 >= 0){
                dist[i][j] = Math.min(dist[i][j], dist[i][j-1] + 1);
            }
        }
    }
    //向右向上遍历
    for(int i = m-1; i >= 0; i--){
        for(int j = 0; j < n; j++){
            if(i + 1 < m){
                dist[i][j] = Math.min(dist[i][j], dist[i+1][j] + 1);
            }  
            if(j - 1 >= 0){
                dist[i][j] = Math.min(dist[i][j], dist[i][j-1] + 1);
            }
        }
    }
    //向左向上遍历
    for(int i =m-1; i >= 0; i--){
        for(int j = n-1; j >=0; j--){
            if(i + 1 < m){
                dist[i][j] = Math.min(dist[i][j], dist[i+1][j] + 1);
            }  
            if(j + 1 < n){
                dist[i][j] = Math.min(dist[i][j], dist[i][j+1] + 1);
            }
        }
    }
    //向左向下遍历
    for(int i =0; i < m; i++){
        for(int j = n-1; j >= 0; j--){
            if(i - 1 >= 0){
                dist[i][j] = Math.min(dist[i][j], dist[i-1][j] + 1);
            }  
            if(j + 1 < n){
                dist[i][j] = Math.min(dist[i][j], dist[i][j+1] + 1);
            }
        }
    }
    return dist;
}
//动态规划优化,只需要遍历两个方向即可
public int[][] updateMatrix(int[][] mat) {
    int m = mat.length, n= mat[0].length;
    int[][] dist = new int[m][n];

    for(int i = 0; i < m; i++){
        Arrays.fill(dist[i], Integer.MAX_VALUE / 2);
    }
    //值为0，则距离为0
    for(int i = 0; i < m; i++){
        for(int j = 0; j < n; j++){
            if(mat[i][j] == 0){
                dist[i][j] = 0;
            }
        }
    }
    //向右向下遍历
    for(int i =0; i < m; i++){
        for(int j = 0; j < n; j++){
            if(i - 1 >= 0){
                dist[i][j] = Math.min(dist[i][j], dist[i-1][j] + 1);
            }  
            if(j - 1 >= 0){
                dist[i][j] = Math.min(dist[i][j], dist[i][j-1] + 1);
            }
        }
    }
    //向左向上遍历
    for(int i =m-1; i >= 0; i--){
        for(int j = n-1; j >=0; j--){
            if(i + 1 < m){
                dist[i][j] = Math.min(dist[i][j], dist[i+1][j] + 1);
            }  
            if(j + 1 < n){
                dist[i][j] = Math.min(dist[i][j], dist[i][j+1] + 1);
            }
        }
    }
    return dist;
}
```

### 695. 岛屿的最大面积

> 给你一个大小为 m x n 的二进制矩阵 grid 。
>
> 岛屿 是由一些相邻的 1 (代表土地) 构成的组合，这里的「相邻」要求两个 1 必须在 水平或者竖直的四个方向上 相邻。你可以假设 grid 的四个边缘都被 0（代表水）包围着。
>
> 岛屿的面积是岛上值为 1 的单元格的数目。
>
> 计算并返回 grid 中最大的岛屿面积。如果没有岛屿，则返回面积为 0 。

示例一：

```java
输入：grid = [[0,0,1,0,0,0,0,1,0,0,0,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,1,1,0,1,0,0,0,0,0,0,0,0],[0,1,0,0,1,1,0,0,1,0,1,0,0],[0,1,0,0,1,1,0,0,1,1,1,0,0],[0,0,0,0,0,0,0,0,0,0,1,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,0,0,0,0,0,0,1,1,0,0,0,0]]
输出：6
解释：答案不应该是 11 ，因为岛屿只能包含水平或垂直这四个方向上的 1 。
```

示例二：

```java
输入：grid = [[0,0,0,0,0,0,0,0]]
输出：0
```

思路：

> 我们想知道网格中每个连通形状的面积，然后取最大值。
>
> 如果我们在一个土地上，以 444 个方向探索与之相连的每一个土地（以及与这些土地相连的土地），那么探索过的土地总数将是该连通形状的面积。
>
> 为了确保每个土地访问不超过一次，我们每次经过一块土地时，将这块土地的值置为 000。这样我们就不会多次访问同一土地。
>

代码：

```java
class Solution {
    public int maxAreaOfIsland(int[][] grid) {
        int ans = 0;
        for (int i = 0; i != grid.length; ++i) {
            for (int j = 0; j != grid[0].length; ++j) {
                ans = Math.max(ans, dfs(grid, i, j));
            }
        }
        return ans;
    }

    public int dfs(int[][] grid, int cur_i, int cur_j) {
        if (cur_i < 0 || cur_j < 0 || cur_i == grid.length || cur_j == grid[0].length || grid[cur_i][cur_j] != 1) {
            return 0;
        }
        //访问过的设置为0，下次不再访问
        grid[cur_i][cur_j] = 0;
        int[] di = {0, 0, 1, -1};
        int[] dj = {1, -1, 0, 0};
        int ans = 1;
        for (int index = 0; index != 4; ++index) {
            int next_i = cur_i + di[index], next_j = cur_j + dj[index];
            ans += dfs(grid, next_i, next_j);
        }
        return ans;
    }
}
```

### 986. 区间列表的交集

> 给定两个由一些 闭区间 组成的列表，firstList 和 secondList ，其中 firstList[i] = [starti, endi] 而 secondList[j] = [startj, endj] 。每个区间列表都是成对 不相交 的，并且 已经排序 。
>
> 返回这 两个区间列表的交集 。
>
> 形式上，闭区间 [a, b]（其中 a <= b）表示实数 x 的集合，而 a <= x <= b 。
>
> 两个闭区间的 交集 是一组实数，要么为空集，要么为闭区间。例如，[1, 3] 和 [2, 4] 的交集为 [2, 3] 。

示例一：

```java
输入：firstList = [[0,2],[5,10],[13,23],[24,25]], secondList = [[1,5],[8,12],[15,24],[25,26]]
输出：[[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]
```

示例二：

```java
输入：firstList = [[1,3],[5,9]], secondList = []
输出：[]
```

示例三：

```java
输入：firstList = [], secondList = [[4,8],[10,12]]
输出：[]
```

示例四：

```java
输入：firstList = [[1,7]], secondList = [[3,10]]
输出：[[3,7]]
```

思路：

>**方法：归并区间**
>我们称 b 为区间 [a, b] 的末端点。
>在两个数组给定的所有区间中，假设拥有最小末端点的区间是 A[0]。（为了不失一般性，该区间出现在数组 A 中)
>然后，在数组 B 的区间中， A[0] 只可能与数组 B 中的至多一个区间相交。（如果 B 中存在两个区间均与 A[0] 相交，那么它们将共同包含 A[0] 的末端点，但是 B 中的区间应该是不相交的，所以存在矛盾）
>
>**算法**
>如果 A[0] 拥有最小的末端点，那么它只可能与 B[0] 相交。然后我们就可以删除区间 A[0]，因为它不能与其他任何区间再相交了。
>相似的，如果 B[0] 拥有最小的末端点，那么它只可能与区间 A[0] 相交，然后我们就可以将 B[0] 删除，因为它无法再与其他区间相交了。
>我们用两个指针 i 与 j 来模拟完成删除 A[0] 或 B[0] 的操作。

代码：

```java
public int[][] intervalIntersection(int[][] firstList, int[][] secondList) {
    List<int[]> ans = new ArrayList<>();
    int i =0, j = 0;
    while(i < firstList.length && j < secondList.length){
        //如[0,2]与[1,5],找到左端最大值与右端最小值
        int left = Math.max(firstList[i][0], secondList[j][0]);
        int right = Math.min(firstList[i][1], secondList[j][1]);
        //如果左侧值小于右侧值，则有交集
        if(left <= right){
            ans.add(new int[]{left,right});
        }
        //如果A右侧值小于B右侧值，则拿A的下一个集合与B的这个集合进行比较，看是否有交集
        if(firstList[i][1] < secondList[j][1]){
            i++;
        }else{
            //如果B右侧值小于A右侧值，则拿B的下一个集合与A的这个集合进行比较，看是否有交集
            j++;
        }
    }
    return ans.toArray(new int[ans.size()][]);
}
```



### 994. 腐烂的橘子

> 在给定的 m x n 网格 grid 中，每个单元格可以有以下三个值之一：
>
> 值 0 代表空单元格；
> 值 1 代表新鲜橘子；
> 值 2 代表腐烂的橘子。
>
> 每分钟，腐烂的橘子 周围 4 个方向上相邻 的新鲜橘子都会腐烂。
>
> 返回 直到单元格中没有新鲜橘子为止所必须经过的最小分钟数。如果不可能，返回 -1 。

示例一：

```java
输入：grid = [[2,1,1],[1,1,0],[0,1,1]]
输出：4
```

示例二：

```java
输入：grid = [[2,1,1],[0,1,1],[1,0,1]]
输出：-1
解释：左下角的橘子（第 2 行， 第 0 列）永远不会腐烂，因为腐烂只会发生在 4 个正向上。
```

示例三：

```java
输入：grid = [[0,2]]
输出：0
解释：因为 0 分钟时已经没有新鲜橘子了，所以答案就是 0 。
```

代码：

```java
//广度优先搜索
static int[][] dist = new int[][]{{1,0},{-1,0},{0,1},{0,-1}};
public int orangesRotting(int[][] grid) {
    int m = grid.length, n = grid[0].length;
    boolean[][] flag = new boolean[m][n];
    int[][] c = new int[m][n];
    Queue<int[]> queue = new LinkedList<int[]>();
    for(int i = 0; i < m; i++){
        for(int j = 0; j < n; j++){
            if(grid[i][j] == 2){
                queue.offer(new int[]{i,j});
                flag[i][j] = true;
                //c[i][j]标记属于第几层次
                c[i][j] = 1;
            }
        }
    }
    //a：遍历层次；time：遍历时间；
    //表中已有的2是第一层次，遍历a=1的时候time为0，此时被传染腐烂的橘子为第二层次
    int a = 1, time = 0;
    while(!queue.isEmpty()){
        int[] cell = queue.remove();
        int i = cell[0], j = cell[1];
        //一个层次的元素同时遍历，直到一个层次所有的元素都遍历结束了，才会接入下一层次的遍历，时间增加
        if(c[i][j] != a){
            //进入到下一个层次，a值增加
            a++;
            time++;
        }
        for(int d = 0; d < 4; d++){
            int ni = i + dist[d][0];
            int nj = j + dist[d][1];
            if(ni >= 0 && ni < m && nj >= 0 && nj < n && grid[ni][nj] == 1 && !flag[ni][nj]){
                c[ni][nj] = a + 1;	//现在腐烂的是下一个层次
                grid[ni][nj] = 2;
                flag[ni][nj] = true;
                queue.offer(new int[]{ni,nj});
                //把腐烂的元素点加入到队列中，插入到队尾，所以当队列取出a值不同的时候，证明进入到了下一个层次
            }
        } 
    }
    for(int i = 0; i < m; i++){
        for(int j = 0; j < n; j++){
            if(grid[i][j] == 1){
                return -1;
            }
        }
    }
    return time;
}
//官方代码，O(nm),O(nm)
// dr,dc 配合使用得到 grid[r][c] 上grid[r-1][c]左grid[r][c-1]下grid[r+1][c]右grid[r][c+1]的元素
int[] dr = new int[]{-1, 0, 1, 0};
int[] dc = new int[]{0, -1, 0, 1};
public int orangesRotting(int[][] grid) {
    // 获取二维数组的行数row 和 列数 column
    int R = grid.length, C = grid[0].length;
    // queue : all starting cells with rotten oranges
    Queue<Integer> queue = new ArrayDeque();
    Map<Integer, Integer> depth = new HashMap();
    for (int r = 0; r < R; ++r)
        for (int c = 0; c < C; ++c)
            if (grid[r][c] == 2) {
                int code = r * C + c;  // 转化为索引唯一的一维数组
                queue.add(code); //存储腐烂橘子
                depth.put(code, 0); //存储橘子变为腐烂时的时间,key为橘子的一维数组下标，value为变腐烂的时间
            }
    int ans = 0;
    while (!queue.isEmpty()) {
        int code = queue.remove();
        int r = code / C, c = code % C;
        for (int k = 0; k < 4; ++k) {
            int nr = r + dr[k];
            int nc = c + dc[k];
            if (0 <= nr && nr < R && 0 <= nc && nc < C && grid[nr][nc] == 1) {
                grid[nr][nc] = 2;
                int ncode = nr * C + nc;
                queue.add(ncode);
                // 计次的关键 元素 grid[r][c] 的上左下右元素得腐烂时间应该一致
                depth.put(ncode, depth.get(code) + 1);
                ans = depth.get(ncode);
            }
        }
    }
    //检查grid，此时的grid能被感染已经都腐烂了，此时还新鲜的橘子无法被感染
    for (int[] row: grid)
        for (int v: row)
            if (v == 1)
                return -1;
    return ans;
}
```



## 困难题



# 树

## 简单

###  110. 平衡二叉树

> 给定一个二叉树，判断它是否是高度平衡的二叉树。
> 本题中，一棵高度平衡二叉树定义为：
> 一个二叉树*每个节点* 的左右两个子树的高度差的绝对值不超过 1 。

示例一：

```java
输入：root = [3,9,20,null,null,15,7]
输出：true
```

示例二：

```java
输入：root = [1,2,2,3,3,null,null,4,4]
输出：false
```

示例三：

```java
输入：root = []
输出：true
```

代码：

> 思路：自底向上递归的做法类似于后序遍历，对于当前遍历到的节点，先递归地判断其左右子树是否平衡，再判断以当前节点为根的子树是否平衡。如果一棵子树是平衡的，则返回其高度（高度一定是非负整数），否则返回 -1。如果存在一棵子树不平衡，则整个二叉树一定不平衡。

```java
//自顶向下，时间复杂度较高，O(n^2)，其中 n是二叉树中的节点个数
public boolean isBalanced(TreeNode root) {
    if(root == null)
        return true;
    if(!isBalanced(root.left) || !isBalanced(root.right))
        return false;
    if(Math.abs(getHeight(root.left) - getHeight(root.right)) > 1)
        return false;
    return true;
}
public int getHeight(TreeNode root){
    return root == null ? 0 : Math.max(getHeight(root.left), getHeight(root.right)) + 1; 
}

//自底向上，时间复杂度O(n)
public boolean isBalanced(TreeNode root) {
    return getHeight(root) == -1 ? false : true;
}

public int getHeight(TreeNode root){
    if(root == null)
        return 0;
    int leftHeight = getHeight(root.left);
    int rightHeight = getHeight(root.right);
    if(leftHeight == -1 || rightHeight == -1)
        return -1;
    if(Math.abs(leftHeight - rightHeight) > 1)
        return -1;
    return Math.max(leftHeight, rightHeight) + 1;
}
```

> 树的高度：结点n到一个叶子节点的最长路径的长
> 树的深度：结点n到根结点的唯一路径的长
> 先序遍历：根->左->右
> 中序遍历：左->根->右
> 后序遍历：左->右->根（自下而上）

### 617. 合并二叉树

> 给你两棵二叉树： root1 和 root2 。
>
> 想象一下，当你将其中一棵覆盖到另一棵之上时，两棵树上的一些节点将会重叠（而另一些不会）。你需要将这两棵树合并成一棵新二叉树。合并的规则是：如果两个节点重叠，那么将这两个节点的值相加作为合并后节点的新值；否则，不为 null 的节点将直接作为新二叉树的节点。
>
> 返回合并后的二叉树。
>
> 注意: 合并过程必须从两个树的根节点开始。

示例一：

```java
输入：root1 = [1,3,2,5], root2 = [2,1,3,null,4,null,7]
输出：[3,4,5,5,4,null,7]
```

示例二：

```java
输入：root1 = [1], root2 = [1,2]
输出：[2,2]
```

代码：

```java
public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
    if(root1 ==null){
        return root2;
    }
    if(root2 == null){
        return root1;
    }
    TreeNode newTree = new TreeNode(root1.val+root2.val);
    newTree.left = mergeTrees(root1.left, root2.left);
    newTree.right = mergeTrees(root1.right, root2.right);
    return newTree;
}
```



## 中等

### 116. 填充每个节点的下一个右侧节点指针

> 给定一个 **完美二叉树** ，其所有叶子节点都在同一层，每个父节点都有两个子节点。二叉树定义如下：
>
> ```java
> struct Node {
>   int val;
>   Node *left;
>   Node *right;
>   Node *next;
> }
> ```
>
> 填充它的每个 next 指针，让这个指针指向其下一个右侧节点。如果找不到下一个右侧节点，则将 next 指针设置为 NULL。
>
> 初始状态下，所有 next 指针都被设置为 NULL。

示例一：

```java
输入：root = [1,2,3,4,5,6,7]
输出：[1,#,2,3,#,4,5,6,7,#]
解释：给定二叉树如图 A 所示，你的函数应该填充它的每个 next 指针，以指向其下一个右侧节点，如图 B 所示。序列化的输出按层序遍历排列，同一层节点由 next 指针连接，'#' 标志着每一层的结束。
```

示例二：

```java
输入：root = []
输出：[]
```

代码：

```java
public Node connect(Node root) {
    if(root == null){
        return null;
    }
    if(root.left != null){
        root.left.next = root.right;
        if(root.next != null){
            root.right.next = root.next.left;
        }
        connect(root.left);
        connect(root.right);
    }
    return root;
}
//不适用递归的方法：O(n),O(1)
public Node connect(Node root) {
    if(root == null){
        return null;
    }
    Node mostLeft = root, head = root;
    while(mostLeft.left != null){
        head.left.next = head.right;
        if(head.next != null){
            head.right.next = head.next.left;
            head = head.next;
        }else{
            mostLeft = mostLeft.left;
            head = mostLeft;
        }
    }
    return root;
}
```

### 429. N叉树的层序遍历

> 给定一个 N 叉树，返回其节点值的*层序遍历*。（即从左到右，逐层遍历）。
>
> 树的序列化输入是用层序遍历，每组子节点都由 null 值分隔（参见示例）。

示例一：

```java
输入：root = [1,null,3,2,4,null,5,6]
输出：[[1],[3,2,4],[5,6]]
```

示例二：

```java
输入：root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
输出：[[1],[2,3,4,5],[6,7,8,9,10],[11,12,13],[14]]
```

思路：

> 对于「层序遍历」的题目，我们一般使用广度优先搜索。在广度优先搜索的每一轮中，我们会遍历同一层的所有节点。
>
> 具体地，我们首先把根节点 root\textit{root}root 放入队列中，随后在广度优先搜索的每一轮中，我们首先记录下当前队列中包含的节点个数（记为 cnt\textit{cnt}cnt），即表示上一层的节点个数。在这之后，我们从队列中依次取出节点，直到取出了上一层的全部 cnt\textit{cnt}cnt 个节点为止。当取出节点 cur\textit{cur}cur 时，我们将 cur\textit{cur}cur 的值放入一个临时列表，再将 cur\textit{cur}cur 的所有子节点全部放入队列中。
>
> 当这一轮遍历完成后，临时列表中就存放了当前层所有节点的值。这样一来，当整个广度优先搜索完成后，我们就可以得到层序遍历的结果。

代码：

```java
class Node {
    public int val;
    public List<Node> children;
    public Node() {}
    public Node(int _val) {
        val = _val;
    }
    public Node(int _val, List<Node> _children) {
        val = _val;
        children = _children;
    }
};
public List<List<Integer>> levelOrder(Node root) {
    //如果根节点为空，则最终的遍历列表为空
    if(root == null){
        return new ArrayList<List<Integer>>();
    }
    List<List<Integer>> ans = new ArrayList<List<Integer>>();
    //队列存放的是当前层的结点
    Queue<Node> queue = new ArrayDeque<Node>();
    queue.offer(root);
    while(!queue.isEmpty()){
        //确认当前层的结点数
        int cnt = queue.size();
        List<Integer> level = new ArrayList<Integer>();
        //取出队列中cnt个数的结点到level中即当前层的所有结点，遍历这些结点的孩子节点添加到队列中，即需要遍历的下一层的结点
        for(int i = 0; i < cnt; i++){
            Node cur = queue.poll();
            level.add(cur.val);
            //遍历当前结点的孩子结点，并加入到队列中
            for(Node child : cur.children){
                queue.offer(child);
            }
        }
        //cnt是当前层的节点数，遍历结束后退出循环，将这层的结点加入到最后的列表中，如果此时queue为空，即刚刚遍历的结点为叶子节点，否则继续循环，此时队列中存放的都是下一层的结点
        ans.add(level);
    }
    return ans;
}
```



# 交互

## 简单

### 278. 第一个错误的版本

> 你是产品经理，目前正在带领一个团队开发新的产品。不幸的是，你的产品的最新版本没有通过质量检测。由于每个版本都是基于之前的版本开发的，所以错误的版本之后的所有版本都是错的。
>
> 假设你有 n 个版本 [1, 2, ..., n]，你想找出导致之后所有版本出错的第一个错误的版本。
>
> 你可以通过调用 bool isBadVersion(version) 接口来判断版本号 version 是否在单元测试中出错。实现一个函数来查找第一个错误的版本。你应该尽量减少对调用 API 的次数。

示例一:

```java
输入：n = 5, bad = 4
输出：4
解释：
调用 isBadVersion(3) -> false 
调用 isBadVersion(5) -> true 
调用 isBadVersion(4) -> true
所以，4 是第一个错误的版本。
```

示例二：

```java
输入：n = 1, bad = 1
输出：1
```

代码：

```java
public int firstBadVersion(int n) {
    int left = 0;
    int right = n;
    while(left <= right){
        int mid = (right - left) / 2 + left;
        if(isBadVersion(mid) == false){
            left = mid + 1;
        }else{
            right = mid - 1;
        }
    }
    return left;
}
```



## 中等



## 困难



# 字符串

## 简单

### [14. 最长公共前缀](https://leetcode.cn/problems/longest-common-prefix/)

> 编写一个函数来查找字符串数组中的最长公共前缀。
>
> 如果不存在公共前缀，返回空字符串 `""`。

示例一：

```java
输入：strs = ["flower","flow","flight"]
输出："fl"
```

示例二：

```java
输入：strs = ["dog","racecar","car"]
输出：""
解释：输入不存在公共前缀。
```

思路：

> 方法一：横向扫描	O(mn), O(1)
> 依次遍历字符串数组中的每个字符串，对于每个遍历到的字符串，更新最长公共前缀，当遍历完所有的字符串以后，即可得到字符串数组中的最长公共前缀。如果在尚未遍历完所有的字符串时，最长公共前缀已经是空串，则最长公共前缀一定是空串，因此不需要继续遍历剩下的字符串，直接返回空串即可。
>
> 方法二：纵向扫描	O(mn), O(1)
> 纵向扫描时，从前往后遍历所有字符串的每一列，比较相同列上的字符是否相同，如果相同则继续对下一列进行比较，如果不相同则当前列不再属于公共前缀，当前列之前的部分为最长公共前缀。

代码：

```java
// 横向扫描
public String longestCommonPrefix(String[] strs) {
  if(strs == null || strs.length == 0){
    return "";
  }
  String prefix = strs[0];
  int count = strs.length;
  for(int i = 0; i < count; i++){
    prefix = longestCommonPrefix(prefix, strs[i]);
    if(prefix.length() == 0){
      break;
    }
  }
  return prefix;
}
public String longestCommonPrefix(String str1, String str2){
  int length = Math.min(str1.length(), str2.length());
  int index = 0;
  while(index < length && str1.charAt(index) == str2.charAt(index)){
    index++;
  }
  return str1.substring(0, index);
}
// 纵向扫描
public String longestCommonPrefix(String[] strs) {
  if(strs == null || strs.length == 0){
    return "";
  }
  int length = strs[0].length();
  int count = strs.length;
  for(int i = 0; i < length; i++){
    char c = strs[0].charAt(i);
    for(int j = 0; j < count; j++){
      if(i == strs[j].length() || strs[j].charAt(i) != c){
        return strs[0].substring(0, i);
      }
    }
  }
  return strs[0];
}
```



### 344. 反转字符串

> 编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 s 的形式给出。
>
> 不要给另外的数组分配额外的空间，你必须原地修改输入数组、使用 O(1) 的额外空间解决这一问题。

示例一：

```java
输入：s = ["h","e","l","l","o"]
输出：["o","l","l","e","h"]
```

示例二：

```java
输入：s = ["H","a","n","n","a","h"]
输出：["h","a","n","n","a","H"]
```

代码：

```java
//翻转字符串
public void reverseString(char[] s) {
    int left = 0;
    int right = s.length - 1;
    while (left < right) {
        reverse(s, left, right);
        left++;
        right--;
    }
}
public void reverse(char[] s, int left, int right) {
    char temp = s[left];
    s[left] = s[right];
    s[right] = temp;
}
//双指针：O(n)、O(1)
public void reverseString(char[] s) {
    for(int left = 0, right = s.length - 1; left < right; left++, right--){
        char temp = s[left];
        s[left] = s[right];
        s[right] = temp;
    }
}
```

### 557. 反转字符串中的单词

> 给定一个字符串 `s` ，你需要反转字符串中每个单词的字符顺序，同时仍保留空格和单词的初始顺序。

示例一：

```java
输入：s = "Let's take LeetCode contest"
输出："s'teL ekat edoCteeL tsetnoc"
```

示例二：

```java
输入： s = "God Ding"
输出："doG gniD"
```

思路：

> 开辟一个新字符串。然后从头到尾遍历原字符串，直到找到空格为止，此时找到了一个单词，并能得到单词的起止位置。随后，根据单词的起止位置，可以将该单词逆序放到新字符串当中。如此循环多次，直到遍历完原字符串，就能得到翻转后的结果。

代码：

```java
public String reverseWords(String s) {
    StringBuffer stringBuffer = new StringBuffer();
    int i = 0;
    int n = s.length();
    while(i < n){
        int start = i;
        while(i < n && s.charAt(i) != ' '){
            i++;
        }
        for (int j = start; j < i; j++) {
            stringBuffer.append(s.charAt(start + i - j -1));
        }
        while(i < n && s.charAt(i) == ' '){
            i++;
            stringBuffer.append(' ');
        }
    }
    return stringBuffer.toString();
}
```

### 819. 最常见的单词

> 给定一个段落 (paragraph) 和一个禁用单词列表 (banned)。返回出现次数最多，同时不在禁用列表中的单词。
>
> 题目保证至少有一个词不在禁用列表中，而且答案唯一。
>
> 禁用列表中的单词用小写字母表示，不含标点符号。段落中的单词不区分大小写。答案都是小写字母。

示例：

```java
输入: 
paragraph = "Bob hit a ball, the hit BALL flew far after it was hit."
banned = ["hit"]
输出: "ball"
解释: 
"hit" 出现了3次，但它是一个禁用的单词。
"ball" 出现了2次 (同时没有其他单词出现2次)，所以它是段落里出现次数最多的，且不在禁用列表中的单词。 
注意，所有这些单词在段落里不区分大小写，标点符号需要忽略（即使是紧挨着单词也忽略， 比如 "ball,"）， 
"hit"不是最终的答案，虽然它出现次数更多，但它在禁用单词列表中。
```

思路：

>方法一：哈希表 + 计数
>
>为了判断给定段落中的每个单词是否在禁用单词列表中，需要使用哈希集合存储禁用单词列表中的单词。以下将禁用单词列表中的单词称为禁用单词。
>
>遍历段落 paragraph，得到段落中的所有单词，并对每个单词计数，使用哈希表记录每个单词的计数。由于每个单词由连续的字母组成，因此当遇到一个非字母的字符且该字符的前一个字符是字母时，即为一个单词的结束，如果该单词不是禁用单词，则将该单词的计数加 1。如果段落的最后一个字符是字母，则当遍历结束时需要对段落中的最后一个单词判断是否为禁用单词，如果不是禁用单词则将次数加 1。
>
>在遍历段落的过程中，对于每个单词都会更新计数，因此遍历结束之后即可得到最大计数，即出现次数最多的单词的出现次数。
>
>遍历段落之后，遍历哈希表，寻找出现次数等于最大计数的单词，该单词即为最常见的单词。
>

代码：

```java
public String mostCommonWord(String paragraph, String[] banned) {
    Set<String> bannedSet = new HashSet<String>();
    for(String word : banned){
        bannedSet.add(word);
    }
    int maxFrequency = 0;
    Map<String, Integer> frequencies = new HashMap<String, Integer>();
    StringBuffer sb = new StringBuffer();
    int length = paragraph.length();
    for(int i = 0; i <= length; i++){
        if(i < length && Character.isLetter(paragraph.charAt(i))){
            sb.append(Character.toLowerCase(paragraph.charAt(i)));
        }else if(sb.length() > 0){
            String word = sb.toString();
            if(!bannedSet.contains(word)){
                int frequency = frequencies.getOrDefault(word,0) + 1;
                frequencies.put(word, frequency);
                maxFrequency = Math.max(maxFrequency, frequency);
            }
            sb.setLength(0);
        }
    }
    String mostCommon = "";
    Set<Map.Entry<String, Integer>> entries = frequencies.entrySet();
    for(Map.Entry<String, Integer> entry : entries){
        String word = entry.getKey();
        int frequency = entry.getValue();
        if(frequency == maxFrequency){
            mostCommon = word;
            break;
        }
    }
    return mostCommon;
}
```

### 821. 字符的最短距离

> 给你一个字符串 s 和一个字符 c ，且 c 是 s 中出现过的字符。
>
> 返回一个整数数组 answer ，其中 answer.length == s.length 且 answer[i] 是 s 中从下标 i 到离它 最近 的字符 c 的 距离 。
>
> 两个下标 i 和 j 之间的 距离 为 abs(i - j) ，其中 abs 是绝对值函数。

示例一：

```java
输入：s = "loveleetcode", c = "e"
输出：[3,2,1,0,1,0,0,1,2,2,1,0]
解释：字符 'e' 出现在下标 3、5、6 和 11 处（下标从 0 开始计数）。
距下标 0 最近的 'e' 出现在下标 3 ，所以距离为 abs(0 - 3) = 3 。
距下标 1 最近的 'e' 出现在下标 3 ，所以距离为 abs(1 - 3) = 2 。
对于下标 4 ，出现在下标 3 和下标 5 处的 'e' 都离它最近，但距离是一样的 abs(4 - 3) == abs(4 - 5) = 1 。
距下标 8 最近的 'e' 出现在下标 6 ，所以距离为 abs(8 - 6) = 2 。
```

示例二：

```java
输入：s = "aaab", c = "b"
输出：[3,2,1,0]
```

思路：

>**方法一：两次遍历**
>问题可以转换成，对 s的每个下标 i，求
>s[i]到其左侧最近的字符 c 的距离
>s[i]到其右侧最近的字符 c 的距离
>这两者的最小值。
>对于前者，我们可以从左往右遍历 s，若 s[i]=c 则记录下此时字符 c 的的下标 idx。遍历的同时更新 answer[i]=i−idx。
>对于后者，我们可以从右往左遍历 s，若 s[i]=c 则记录下此时字符 c 的的下标 idx。遍历的同时更新 answer[i]=min ⁡(answer[i],idx−i)。
>代码实现时，在开始遍历的时候 idx 可能不存在，为了简化逻辑，我们可以用 −n或 2n 表示，这里 n 是 s 的长度。

代码：

```java
//暴力求解
public int[] shortestToChar(String s, char c) {
    int length = s.length();
    int[] ans = new int[length];
    for(int i =0; i < length; i++){
        ans[i] = length;
    }
    for(int i = 0; i < length; i++){
        if(s.charAt(i) == c){
            for(int j = 0; j < length; j++){
                ans[j] = Math.min(ans[j], Math.abs(i-j));
            }
        }
    }
    return ans;
}
//官方题解，两次遍历：O(n),O(1)
public int[] shortestToChar(String s, char c) {
    int length = s.length();
    int[] ans = new int[length];
    //从左至右遍历数组，记录元素与左侧最近的c的距离
    for(int i = 0, idx = -length; i < length; i++){
        if(s.charAt(i) == c){
            idx = i;
        }
        ans[i] = i - idx;
    }
    //从右至左遍历数组，比较元素与左右侧最近的c的距离
    for(int i = length - 1, idx = 2 * length; i >= 0; i--){
        if(s.charAt(i) == c){
            idx = i;
        }
        ans[i] = Math.min(ans[i], idx - i);
    }
    return ans;
}
```

### 824. 山羊拉丁文

> 给你一个由若干单词组成的句子 sentence ，单词间由空格分隔。每个单词仅由大写和小写英文字母组成。
>
> 请你将句子转换为 “山羊拉丁文（Goat Latin）”（一种类似于 猪拉丁文 - Pig Latin 的虚构语言）。山羊拉丁文的规则如下：
>
> 如果单词以元音开头（'a', 'e', 'i', 'o', 'u'），在单词后添加"ma"。
>     例如，单词 "apple" 变为 "applema" 。
> 如果单词以辅音字母开头（即，非元音字母），移除第一个字符并将它放到末尾，之后再添加"ma"。
>     例如，单词 "goat" 变为 "oatgma" 。
> 根据单词在句子中的索引，在单词最后添加与索引相同数量的字母'a'，索引从 1 开始。
>     例如，在第一个单词后添加 "a" ，在第二个单词后添加 "aa" ，以此类推。
>
> 返回将 sentence 转换为山羊拉丁文后的句子。

示例一：

```java
输入：sentence = "I speak Goat Latin"
输出："Imaa peaksmaaa oatGmaaaa atinLmaaaaa"
```

示例二：

```java
输入：sentence = "The quick brown fox jumped over the lazy dog"
输出："heTmaa uickqmaaa rownbmaaaa oxfmaaaaa umpedjmaaaaaa overmaaaaaaa hetmaaaaaaaa azylmaaaaaaaaa ogdmaaaaaaaaaa"
```

思路:

>**方法一：找到每一个单词 + 模拟**
>
>我们可以对给定的字符串 sentence进行一次遍历，找出其中的每一个单词，并根据题目的要求进行操作。
>
>在寻找单词时，我们可以使用语言自带的 split()函数，将空格作为分割字符，得到所有的单词。为了节省空间，我们也可以直接进行遍历：每当我们遍历到一个空格或者到达 sentence 的末尾时，我们就找到了一个单词。
>当我们得到一个单词 w 后，我们首先需要判断 w 的首字母是否为元音字母。我们可以使用一个哈希集合 vowels 存储所有的元音字母 aeiouAEIOU，这样只需要判断 w 的首字母是否在 vowels 中。如果是元音字母，那么单词本身保持不变；如果是辅音字母，那么需要首字母移到末尾，这里使用语言自带的字符串切片函数即可。在这之后，我们需要在末尾添加 m\text{m}m 以及若干个 a\text{a}a，因此可以使用一个变量 cnt记录需要添加的 a的个数，它的初始值为 111，每当我们得到一个单词，就将它的值增加 1。

代码：

```java
class Solution {
    public String toGoatLatin(String sentence) {
        String[] words = sentence.split(" ");
        StringBuffer ans = new StringBuffer();
        for(int i = 0; i < words.length; i++){
            String word = words[i];
            StringBuffer sb = new StringBuffer();
            if(isY(word.charAt(0))){
                sb.append(word + "ma");
            }else{
                sb.append(word.substring(1) + word.charAt(0) + "ma");
            }
            for(int j = 0; j <= i; j++){
                sb.append("a");
            }
            ans.append(sb);
            if(i != (words.length - 1))
                ans.append(" ");
        }
        return ans.toString();
    }
    //判断是否是元音字母
    public boolean isY(char c){
        char[] ys = new char[]{'a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O','U'};
        for(char ch : ys){
            if(c == ch){
                return true;
            }
        }
        return false;
    }
}
//集合存放元音字母
public String toGoatLatin(String sentence) {
    Set<Character> ys = new HashSet<>();
    ys.add('a');
    ys.add('e');
    ys.add('i');
    ys.add('o');
    ys.add('u');
    ys.add('A');
    ys.add('E');
    ys.add('I');
    ys.add('O');
    ys.add('U');
    String[] words = sentence.split(" ");
    StringBuffer ans = new StringBuffer();
    for(int i = 0; i < words.length; i++){
        String word = words[i];
        StringBuffer sb = new StringBuffer();
        if(ys.contains(word.charAt(0))){
            sb.append(word + "ma");
        }else{
            sb.append(word.substring(1) + word.charAt(0) + "ma");
        }
        for(int j = 0; j <= i; j++){
            sb.append("a");
        }
        ans.append(sb);
        if(i != words.length - 1){
            ans.append(" ");
        }
    }
    return ans.toString();
}
//官方题解：O(N^2),O(N^2)
 public String toGoatLatin(String sentence) {
     Set<Character> vowels = new HashSet<Character>() {{
         add('a');
         add('e');
         add('i');
         add('o');
         add('u');
         add('A');
         add('E');
         add('I');
         add('O');
         add('U');
     }};
     int n = sentence.length();
     int i = 0, cnt = 0;
     StringBuffer ans = new StringBuffer();
     while (i < n) {
         int j = i;
         while (j < n && sentence.charAt(j) != ' ') {
             ++j;
         }
         ++cnt;
         if (vowels.contains(sentence.charAt(i))) {
             ans.append(sentence.substring(i, j));
         } else {
             ans.append(sentence.substring(i + 1, j));
             ans.append(sentence.charAt(i));
         }
         ans.append("ma");
         for (int k = 0; k < cnt; ++k) {
             ans.append('a');
         }
         if(j != n)
             ans.append(" ");
         i = j + 1;
     }
     return ans.toString();
 }
```



### 844. 比较含退格的字符串

> 给定 s 和 t 两个字符串，当它们分别被输入到空白的文本编辑器后，如果两者相等，返回 true 。# 代表退格字符。
>
> 注意：如果对空文本输入退格字符，文本继续为空。

示例一：

```java
输入：s = "ab#c", t = "ad#c"
输出：true
解释：s 和 t 都会变成 "ac"。
```

示例二：

```java
输入：s = "ab##", t = "c#d#"
输出：true
解释：s 和 t 都会变成 ""。
```

示例三：

```java
输入：s = "a#c", t = "b"
输出：false
解释：s 会变成 "c"，但 t 仍然是 "b"。
```

思路：

> **方法一：重构字符串**
> 最容易想到的方法是将给定的字符串中的退格符和应当被删除的字符都去除，还原给定字符串的一般形式。然后直接比较两字符串是否相等即可。
> 具体地，我们用栈处理遍历过程，每次我们遍历到一个字符：
> 如果它是退格符，那么我们将栈顶弹出；
> 如果它是普通字符，那么我们将其压入栈中。
>
> **方法二：双指针**
> 一个字符是否会被删掉，只取决于该字符后面的退格符，而与该字符前面的退格符无关。因此当我们逆序地遍历字符串，就可以立即确定当前字符是否会被删掉。
> 具体地，我们定义 skip 表示当前待删除的字符的数量。每次我们遍历到一个字符：
> 若该字符为退格符，则我们需要多删除一个普通字符，我们让 skip 加 1；
> 若该字符为普通字符：
>     若 skip为 0，则说明当前字符不需要删去；
>     若 skip不为 0，则说明当前字符需要删去，我们让 skip 减 1。
> 这样，我们定义两个指针，分别指向两字符串的末尾。每次我们让两指针逆序地遍历两字符串，直到两字符串能够各自确定一个字符，然后将这两个字符进行比较。重复这一过程直到找到的两个字符不相等，或遍历完字符串为止。

代码：

```java
//重构字符串：O(M+N),O(N+M)
class Solution {
    public boolean backspaceCompare(String s, String t) {
        return build(s).equals(build(t));
    }
    public String build(String str){
        StringBuffer sb = new StringBuffer();
        int length = str.length();
        for(int i = 0; i < length; i++){
            if(str.charAt(i) != '#'){
                sb.append(str.charAt(i));
            }else{
                if(sb.length() != 0){
                    sb.deleteCharAt(sb.length() - 1);
                }
                
            }
        }
        return sb.toString();
    }
}
//双指针：O(M+N),O(1)
public boolean backspaceCompare(String s, String t) {
    int i = s.length() - 1;
    int j = t.length() - 1;
    int skipS = 0, skipT = 0;
    while(i >= 0 || j >= 0){
        // 先找到 s 中第一个需要比较的字符（即去除 # 影响后的第一个待比较字符）
        while(i > 0){
            if(s.charAt(i) == '#'){
                skipS++;
                i--;
            }else if(skipS > 0){
                skipS--;
                i--;
            }else{
                break;
            }
        }
        // 再找到 t 中第一个需要比较的字符（即去除 # 影响后的第一个待比较字符）
        while(j > 0){
            if(t.charAt(j) == '#'){
                skipT++;
                j--;
            }else if(skipT > 0){
                skipT--;
                j--;
            }else{
                break;
            }
        }
        // 然后开始比较,注意有下面这个 if 条件的原因是：如果 index = 0 位置上为 '#'，则 i, j 会为 -1
        // 而 index = -1 的情况应当处理。
        if(i >= 0 && j >= 0){
            if(s.charAt(i) != t.charAt(j)){
                // 如果待比较字符不同，return false
                return false;
            }
        }else{
            // (i >= 0 && j >= 0) 为 false 情况为
            // 1. i < 0 && j >= 0
            // 2. j < 0 && i >= 0
            // 3. i < 0 && j < 0
            // 其中，第 3 种情况为符合题意情况，因为这种情况下 s 和 t 都是 index = 0 的位置为 '#' 而这种情况下
            // 退格空字符即为空字符，也符合题意，应当返回 True。
            // 但是，情况 1 和 2 不符合题意，因为 s 和 t 其中一个是在 index >= 0 处找到了待比较字符，另一个没有找到
            // 这种情况显然不符合题意，应当返回 False，下式便处理这种情况。
            if(i >= 0 || j >= 0){
                return false;
            }
        }
    }
    return true;
}
```



## 中等

### 3. 无重复字符的最长子串

> 给定一个字符串 `s` ，请你找出其中不含有重复字符的 **最长子串** 的长度。

示例一：

```java
输入: s = "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

示例二：

```java
输入: s = "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```

示例三：

```java
输入: s = "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

思路：

> 假设我们选择字符串中的第 k 个字符作为起始位置，并且得到了不包含重复字符的最长子串的结束位置为 rk。那么当我们选择第 k+1 个字符作为起始位置时，首先从 k+1 到 rk 的字符显然是不重复的，并且由于少了原本的第 k 个字符，我们可以尝试继续增大 rk，直到右侧出现了重复字符为止。
>
> 这样一来，我们就可以使用「滑动窗口」来解决这个问题了：
>
> 我们使用两个指针表示字符串中的某个子串（或窗口）的左右边界，其中左指针代表着上文中枚举子串的起始位置，而右指针即为上文中的 rk；
>
> 在每一步的操作中，我们会将左指针向右移动一格，表示 我们开始枚举下一个字符作为起始位置，然后我们可以不断地向右移动右指针，但需要保证这两个指针对应的子串中没有重复的字符。在移动结束后，这个子串就对应着 以左指针开始的，不包含重复字符的最长子串。我们记录下这个子串的长度；
>
> 在枚举结束后，我们找到的最长的子串的长度即为答案。

代码：

```java
//滑动窗口
public int lengthOfLongestSubstring(String s) {
    // 哈希集合，记录每个字符是否出现过
    Set<Character> occ = new HashSet<Character>();
    int n = s.length();
    // 右指针，初始值为 -1，相当于我们在字符串的左边界的左侧，还没有开始移动
    int rk = -1, ans = 0;
    for (int i = 0; i < n; ++i) {
        if (i != 0) {
            // 左指针向右移动一格，移除一个字符
            occ.remove(s.charAt(i - 1));
        }
        while (rk + 1 < n && !occ.contains(s.charAt(rk + 1))) {
            // 不断地移动右指针
            occ.add(s.charAt(rk + 1));
            ++rk;
        }
        // 第 i 到 rk 个字符是一个极长的无重复字符子串
        ans = Math.max(ans, rk - i + 1);
    }
    return ans;
}
```

### 385. 迷你语法分析器

> 给定一个字符串 s 表示一个整数嵌套列表，实现一个解析它的语法分析器并返回解析的结果 NestedInteger 。
>
> 列表中的每个元素只可能是整数或整数嵌套列表
>

示例一：

```java
输入：s = "324",
输出：324
解释：你应该返回一个 NestedInteger 对象，其中只包含整数值 324。
```

示例二：

```java
输入：s = "[123,[456,[789]]]",
输出：[123,[456,[789]]]
解释：返回一个 NestedInteger 对象包含一个有两个元素的嵌套列表：
1. 一个 integer 包含值 123
2. 一个包含两个元素的嵌套列表：
    i.  一个 integer 包含值 456
    ii. 一个包含一个元素的嵌套列表
         a. 一个 integer 包含值 789
```

思路：

> 方法一：深度优先搜索
> 根据题意，一个 NestedInteger实例只能包含下列两部分之一：1）一个整数；2）一个列表，列表中的每个元素都是一个 NestedInteger 实例。据此，NestedInteger 是通过递归定义的，因此也可以用递归的方式来解析。
> 从左至右遍历 s，
> 如果第一位是 ‘[’ 字符，则表示待解析的是一个列表，从 ‘[’ 后面的字符开始又是一个新的 NestedInteger实例，我们仍调用解析函数来解析列表的元素，调用结束后如果遇到的是 ,字符，表示列表仍有其他元素，需要继续调用。如果是 ‘]’ 字符，表示这个列表已经解析完毕，可以返回 NestedInteger实例。
> 否则，则表示待解析的 NestedInteger只包含一个整数。我们可以从左至右解析这个整数，并注意是否是负数，直到遍历完或者遇到非数字字符（‘]’ 或 ‘,’），并返回NestedInteger实例。
>
> 方法二：栈
> 上述递归的思路也可以用栈来模拟。从左至右遍历 s，如果遇到 ‘[’，则表示是一个新的 NestedInteger实例，需要将其入栈。如果遇到 ‘]’ 或‘,’，则表示是一个数字或者 NestedInteger实例的结束，需要将其添加入栈顶的 NestedInteger 实例。最后需返回栈顶的实例。

代码：

```java
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * public interface NestedInteger {
 *     // Constructor initializes an empty nested list.
 *     public NestedInteger();
 *
 *     // Constructor initializes a single integer.
 *     public NestedInteger(int value);
 *
 *     // @return true if this NestedInteger holds a single integer, rather than a nested list.
 *     public boolean isInteger();
 *
 *     // @return the single integer that this NestedInteger holds, if it holds a single integer
 *     // Return null if this NestedInteger holds a nested list
 *     public Integer getInteger();
 *
 *     // Set this NestedInteger to hold a single integer.
 *     public void setInteger(int value);
 *
 *     // Set this NestedInteger to hold a nested list and adds a nested integer to it.
 *     public void add(NestedInteger ni);
 *
 *     // @return the nested list that this NestedInteger holds, if it holds a nested list
 *     // Return empty list if this NestedInteger holds a single integer
 *     public List<NestedInteger> getList();
 * }
 */
//深度优先搜索
class Solution {
    //初始遍历的索引值为0
    int index = 0;
    public NestedInteger deserialize(String s) {
        //如果第一个字符是'[',则证明这是一个列表，直到遇到]才代表一个元素
        //表明之后的一段是个NestedInteger列表
        if(s.charAt(index) == '['){
            //继续向下遍历
            index++;
            //主函数的总nested
            NestedInteger ni = new NestedInteger();
            //终止条件是，在本层遇到一个“]”，表示的是本层的嵌套解析结束
            while(s.charAt(index) != ']'){
                //将递归得到的NestedInteger值加入到已建好的ni列表中
                ni.add(deserialize(s));
                //如果当前值为','，则证明后续仍有同组的数字
                if(s.charAt(index) == ','){
                    //索引值增加，继续遍历下一个列表中的数
                    index++;
                }
            }
            //由于此时start指向的位置是“]”，需要右移
            index++;
            return ni;
        }else{
            //本层是单个数字
            //确定这层中的数是正数还是负数，默认是整数。设为false
            boolean negative = false;
            if(s.charAt(index) == '-'){
                //寻找本层数字的第一个数
                index++;
                negative = true;
            }
            int num = 0;
            //Character.isDigit(s.charAt(index))确当现在遍历的字符是数字，如果不是数字则跳出循环
            while(index < s.length() && Character.isDigit(s.charAt(index))){
                //每多一位，前面的数应该*10，表示上一位的数字，s.charAt(index) - '0'表示新加入的个位数字
                num = num * 10 + s.charAt(index) - '0';
                index++;
            }
            //如果这层数字为负数，将num值*（-1）
            if(negative){
                num *= -1;
            }
            //返回本层的数字
            return new NestedInteger(num);
        }
    }
}

//栈
class Solution {
    public NestedInteger deserialize(String s) {
        if(s.charAt(0) != '['){
            //第一个字符不是[，表示只有数字，直接返回即可
            return new NestedInteger(Integer.parseInt(s));
        }
        //定义一个空栈
        Deque<NestedInteger> stack = new ArrayDeque<NestedInteger>();
        //判断数字正负
        boolean negative = false;
        int num = 0;
        for(int i = 0; i < s.length(); i++){
            char c = s.charAt(i);
            if(c == '-'){
                negative = true;
            }else if(Character.isDigit(c)){
                num = num * 10 + c - '0'; 
            }else if(c == '['){
                //表示的是nestedList的开始，需要建立一个包裹，注意，栈顶的永远都是待填满的nest
                stack.push(new NestedInteger());
            }else if(c == ',' || c == ']'){
                //此时代表的，1、要么是栈顶的nest遇到了末尾（前一个二级nest已经放进去了）；
                //2、要么是前一个对象刚刚解析完，需要装到更高一级的nest中
                //此时表示情况1，将新的nest放入到栈顶列表中
                if(Character.isDigit(s.charAt(i-1))){
                    if(negative){
                        num *= -1;
                    }
                    stack.peek().add(new NestedInteger(num));
                }
                num = 0;
                negative = false;
                //此时表示的是情况2，列表中所有元素解析结束，将栈顶列表取出，此时新的栈顶列表是上一级NestedInteger列表，将刚刚取出的放入进去，ce
                if(c == ']' && stack.size() > 1){
                    NestedInteger ni = stack.pop();
                    stack.peek().add(ni);
                }
            }
        }
        return stack.pop();
    }
}
```

### 388. 文件的最长绝对路径

> ![image-20220420004557749](leecode%E5%81%9A%E9%A2%98%E7%AC%94%E8%AE%B0.assets/image-20220420004557749-16503867595235.png)

示例一：

<img src="leecode%E5%81%9A%E9%A2%98%E7%AC%94%E8%AE%B0.assets/image-20220420004704906.png" alt="image-20220420004704906" style="zoom:50%;" />

```java
输入：input = "dir\n\tsubdir1\n\tsubdir2\n\t\tfile.ext"
输出：20
解释：只有一个文件，绝对路径为 "dir/subdir2/file.ext" ，路径长度 20
```

示例二：

<img src="leecode%E5%81%9A%E9%A2%98%E7%AC%94%E8%AE%B0.assets/image-20220420004736147.png" alt="image-20220420004736147" style="zoom:50%;" />

```java
输入：input = "dir\n\tsubdir1\n\t\tfile1.ext\n\t\tsubsubdir1\n\tsubdir2\n\t\tsubsubdir2\n\t\t\tfile2.ext"
输出：32
解释：存在两个文件：
"dir/subdir1/file1.ext" ，路径长度 21
"dir/subdir2/subsubdir2/file2.ext" ，路径长度 32
返回 32 ，因为这是最长的路径
```

示例三：

```java
输入：input = "a"
输出：0
解释：不存在任何文件
```

示例四：

```java
输入：input = "file1.txt\nfile2.txt\nlongfile.txt"
输出：12
解释：根目录下有 3 个文件。
因为根目录中任何东西的绝对路径只是名称本身，所以答案是 "longfile.txt" ，路径长度为 12
```

思路：

>**方法一：栈**
>题目中需求出文件系统中文件绝对路径的最大长度。首先观察文件绝对路径的特征，文件名一定包含 ‘.’，此时文件的绝对路径为 x/y/.../a.b，其中 x,y 代表文件夹的名称，a.b 代表文件名。我们可以观察到文件系统实际为树形结构，文件一定为树中的叶子节点，文件夹可以为根节点也可以为叶子节点，题目中给定的文件系统字符串实际为树按照前序遍历的结果，连续的 ‘\t’ 的个数代表当前节点的深度，相邻的文件名之间都以 ‘\n’ 进行隔开。
>假设当前的路径为 x/y/z，其中 x,y,z 的文件名长度为分别为 lx,ly,lz，则路径 x, x/y, x/y/z的长度分别为 lx,lx+ly+1,lx+ly+lz+2。我们利用栈保存当前已遍历路径的长度，栈中元素的个数即为当前路径的深度，栈顶元素即为当前路径的长度。设根节点的深度为 1，字符串中连续的 ‘\t’ 的个数加 1 即为当前节点的深度 depth，设当前节点的文件名为 q，当前节点的文件名长度为 lp，根据节点深度 depth 有以下判断：
>如果当前节点的深度大于当前路径的深度，则表明当前节点为栈顶节点的孩子节点，设当前栈顶节点的长度为 t，栈顶节点的路径为 p，则此时当前文件的路径应该为 p/q，则此时当前文件的路径长度为 t+lp+1。
>如果当前节点的深度小于当前路径的深度，则表明当前节点并不是栈顶节点的孩子节点，按照先序遍历的顺序，则此时需要进行回退直到栈顶节点为当前节点的父亲节点，然后再求出当前节点的路径与长度。
>由于题目只需要求出文件的长度即可，因此我们在实际运算中在栈中不需要保存完整的路径名称，只需要保存每个路径的长度即可。检测当前节点的文件名的长度并标记当前的文件名是文件还是文件夹，如果当前的字符串为文件，则求出当前文件绝对路径的长度。遍历所有可能的文件长度，即可找到文件绝对路径的最大长度。
>
>**方法二：遍历**
>假设当前的路径为 x/y/z，其中 x,y,z 的文件名长度为分别为 lx,ly,lz，则路径 x, x/y, x/y/z 的长度分别为 lx,lx+ly+1,lx+ly+lz+2。我们用 level[i] 保存当前已遍历路径中第 iii 层目录的长度。设根目录为第 1 层，字符串中连续的 ‘\t’ 的个数加 1即为当前路径的层次深度 depth，设当前节点的文件名为 p，当前节点的文件名长度为 lp，根据当前文件的层次深度 depth 有以下判断：
>当前文件绝对路径也就等于当前路径中第 depth−1层的绝对路径加上 ‘/’，然后再加上当前的文件名，当前文件绝对路径的长度也就等于 level[depth−1]+1+lp。特殊情况需要处理，当前为根目录时，不需要添加额外的 ‘/’。如果当前文件名为文件夹时，则需要更新当前第 depth 层的路径长度。
>由于每次目录按照向下遍历时，是按照层级目录往下进行遍历的，即每次只能遍历完第 i 层目录，才能遍历到第 i+1 层目录，因此我们在向下进行遍历第 i 层目录时，实际上前 i−1 层的目录路径不会发生改变。当从 i 层目录回退到第 j 层时，i>j，此时前 i−1 层绝对路径是保持不变的，因此可以直接利用已经保存的前 i−1 层的绝对路径长度。
>由于题目只需要求出文件的长度即可，因此我们在实际运算中不需要保存完整的路径名称，只需要保存每个路径的长度即可。检测当前节点的文件名的长度并标记当前的文件名是文件还是文件夹，如果当前的文件名为文件，则求出当前文件绝对路径的长度。遍历所有可能的文件路径长度，即可找到文件绝对路径的最大长度。

代码：

```java
//迭代：O(n),O(n)
public int lengthLongestPath(String input) {
    int n = input.length();
    int pos = 0;
    int ans = 0;
    int[] level = new int[n+1];
    while(pos < n){
        int depth = 1;
        while(pos < n && input.charAt(pos) == '\t'){
            depth++;
            pos++;
        }
        int len = 0;
        boolean isFile = false;
        while(pos < n && input.charAt(pos) != '\n'){
            if(input.charAt(pos) == '.'){
                isFile = true;
            }
            len++;
            pos++;
        }
        pos++;
        if(depth > 1){
            len += level[depth-1] + 1;
        }
        if(isFile){
            ans = Math.max(ans, len);
        }else{
            level[depth] = len;
        }
    }
    return ans;
}
//栈:O(n),O(n)
public int lengthLongestPath(String input) {
    int n = input.length();
    int pos = 0;
    int ans = 0;
    Deque<Integer> stack = new ArrayDeque<Integer>();
    while(pos < n){
        int depth = 1;
        while(pos < n && input.charAt(pos) == '\t'){
            depth++;
            pos++;
        }
        int len = 0;
        boolean isFile = false;
        while(pos < n && input.charAt(pos) != '\n'){
            if(input.charAt(pos) == '.'){
                isFile = true;
            }
            len++;
            pos++;
        }
        pos++;
        while(stack.size() >= depth){
            stack.pop();
        }
        if(!stack.isEmpty()){
            len += stack.peek() + 1;
        }
        if(isFile){
            ans = Math.max(len, ans);
        }else{
            stack.push(len);
        }
    }
    return ans;
}
```

### 438. 找到字符串中所有字母异位词

> 给定两个字符串 s 和 p，找到 s 中所有 p 的 异位词 的子串，返回这些子串的起始索引。不考虑答案输出的顺序。
>
> 异位词 指由相同字母重排列形成的字符串（包括相同的字符串）。

示例一：

```java
输入: s = "cbaebabacd", p = "abc"
输出: [0,6]
解释:
起始索引等于 0 的子串是 "cba", 它是 "abc" 的异位词。
起始索引等于 6 的子串是 "bac", 它是 "abc" 的异位词。
```

示例二：

```java
输入: s = "abab", p = "ab"
输出: [0,1,2]
解释:
起始索引等于 0 的子串是 "ab", 它是 "ab" 的异位词。
起始索引等于 1 的子串是 "ba", 它是 "ab" 的异位词。
起始索引等于 2 的子串是 "ab", 它是 "ab" 的异位词。
```

思路：

>**方法一：滑动窗口**
>根据题目要求，我们需要在字符串 s 寻找字符串 p 的异位词。因为字符串 p 的异位词的长度一定与字符串 p 的长度相同，所以我们可以在字符串 s 中构造一个长度为与字符串 p 的长度相同的滑动窗口，并在滑动中维护窗口中每种字母的数量；当窗口中每种字母的数量与字符串 p 中每种字母的数量相同时，则说明当前窗口为字符串 p 的异位词。
>在算法的实现中，我们可以使用数组来存储字符串 p 和滑动窗口中每种字母的数量。
>当字符串 s 的长度小于字符串 p 的长度时，字符串 s 中一定不存在字符串 p 的异位词。但是因为字符串 s 中无法构造长度与字符串 p 的长度相同的窗口，所以这种情况需要单独处理。
>
>**方法二：优化的滑动窗口**
>在方法一的基础上，我们不再分别统计滑动窗口和字符串 p 中每种字母的数量，而是统计滑动窗口和字符串 p 中每种字母数量的差；并引入变量 differ 来记录当前窗口与字符串 p 中数量不同的字母的个数，并在滑动窗口的过程中维护它。
>在判断滑动窗口中每种字母的数量与字符串 p 中每种字母的数量是否相同时，只需要判断 differ 是否为零即可。

代码：

```java
//滑动窗口：O(m+(n−m)×Σ)，O(Σ)
public List<Integer> findAnagrams(String s, String p) {
    int sn = s.length(), pn = p.length();
    List<Integer> ans = new ArrayList<>();
    if(sn < pn){
        return ans;
    }
    int[] sCount = new int[26];
    int[] pCount = new int[26];
    for(int i = 0; i < pn; i++){
        sCount[s.charAt(i) - 'a']++;
        pCount[p.charAt(i) - 'a']++;
    }
    if(Arrays.equals(sCount, pCount)){
        ans.add(0);
    }
    for(int i = 0; i < sn - pn; i++){
        sCount[s.charAt(i) - 'a']--;
        sCount[s.charAt(i+pn) - 'a']++;
        if(Arrays.equals(sCount, pCount)){
            ans.add(i+1);
        }
    }
    return ans;
}
//滑动窗口优化：O(n+m+Σ)，O(Σ)
public List<Integer> findAnagrams(String s, String p) {
    int sLen = s.length(), pLen = p.length();
    if (sLen < pLen) {
        return new ArrayList<Integer>();
    }
    List<Integer> ans = new ArrayList<Integer>();
    int[] count = new int[26];
    for (int i = 0; i < pLen; ++i) {
        ++count[s.charAt(i) - 'a'];
        --count[p.charAt(i) - 'a'];
    }
    int differ = 0;
    for (int j = 0; j < 26; ++j) {
        if (count[j] != 0) {
            //窗口中与p中不相同的字母个数
            ++differ;
        }
    }
    if (differ == 0) {
        ans.add(0);
    }
    for (int i = 0; i < sLen - pLen; ++i) {
        if (count[s.charAt(i) - 'a'] == 1) {  
            //窗口要往右滑动，s的本来都+1了现在要出窗口就-1 如果本来只有一个那么该字母的差值就会变成0 此时不一样的字母个数就少了一个 否则就不管
            // 窗口中字母 s[i] 的数量与字符串 p 中的数量从不同变得相同
            --differ;
        } else if (count[s.charAt(i) - 'a'] == 0) { 
            // 窗口中字母 s[i] 的数量与字符串 p 中的数量从相同变得不同
            //  窗口如果本来为0 那么该字母出去之后就会多一个不一样的字母
            ++differ;
        }
        --count[s.charAt(i) - 'a'];
        // 滑动窗口向右移动，要把右边这个字母加进去
        if (count[s.charAt(i + pLen) - 'a'] == -1) {  
            // 窗口中字母 s[i+pLen] 的数量与字符串 p 中的数量从不同变得相同
            --differ;
        } else if (count[s.charAt(i + pLen) - 'a'] == 0) {  
            // 窗口中字母 s[i+pLen] 的数量与字符串 p 中的数量从相同变得不同
            ++differ;
        }
        ++count[s.charAt(i + pLen) - 'a'];
        // 如果差异个数为0 则说明此时个数相等
        if (differ == 0) {
            ans.add(i + 1);
        }
    }
    return ans;
}
```



### 567. 字符串的排列

> 给你两个字符串 s1 和 s2 ，写一个函数来判断 s2 是否包含 s1 的排列。如果是，返回 true ;否则，返回 false 换句话说，s1 的排列之一是 s2 的 子串 。

示例一：

```java
输入：s1 = "ab" s2 = "eidbaooo"
输出：true
解释：s2 包含 s1 的排列之一 ("ba").
```

示例二：

```java
输入：s1= "ab" s2 = "eidboaoo"
输出：false
```

思路：

> 由于排列不会改变字符串中每个字符的个数，所以只有当两个字符串每个字符的个数均相等时，一个字符串才是另一个字符串的排列。
>
> 根据这一性质，记 s1的长度为 n，我们可以遍历 s2中的每个长度为 n 的子串，判断子串和 s1中每个字符的个数是否相等，若相等则说明该子串是 s1 的一个排列。
>
> 使用两个数组 cnt1和 cnt2，cnt1统计 s1中各个字符的个数，cnt2 统计当前遍历的子串中各个字符的个数。
>
> 由于需要遍历的子串长度均为 n，我们可以使用一个固定长度为 n 的滑动窗口来维护 cnt2：滑动窗口每向右滑动一次，就多统计一次进入窗口的字符，少统计一次离开窗口的字符。然后，判断 cnt1是否与 cnt2相等，若相等则意味着 s1的排列之一是 s2 的子串。
>

代码：

```java
//滑动窗口
public boolean checkInclusion(String s1, String s2) {
    int n = s1.length();
    int m = s2.length();
    int[] count1 = new int[26];
    int[] count2 = new int[26];
    if(n > m){
        return false;
    }
    for (int i = 0; i < n; i++) {
        count1[s1.charAt(i) - 'a']++;
        count2[s2.charAt(i) - 'a']++;
    }
    if(Arrays.equals(count1,count2)){
        return true;
    }

    for (int i = n; i < m ; i++) {
        count2[s2.charAt(i)-'a']++;
        count2[s2.charAt(i-n)-'a']--;
        if(Arrays.equals(count1,count2))
            return true;
    }
    return false;
}
//双指针
public boolean checkInclusion(String s1, String s2) {
    int n = s1.length(), m = s2.length();
    if (n > m) {
        return false;
    }
    int[] cnt = new int[26];
    for (int i = 0; i < n; ++i) {
        --cnt[s1.charAt(i) - 'a'];
    }
    int left = 0;
    for (int right = 0; right < m; ++right) {
        int x = s2.charAt(right) - 'a';
        ++cnt[x];
        while (cnt[x] > 0) {
            --cnt[s2.charAt(left) - 'a'];
            ++left;
        }
        if (right - left + 1 == n) {
            return true;
        }
    }
    return false;
}
```

### 2024. 考试的最大困扰度

> 一位老师正在出一场由 n 道判断题构成的考试，每道题的答案为 true （用 'T' 表示）或者 false （用 'F' 表示）。老师想增加学生对自己做出答案的不确定性，方法是 最大化 有 连续相同 结果的题数。（也就是连续出现 true 或者连续出现 false）。
>
> 给你一个字符串 answerKey ，其中 answerKey[i] 是第 i 个问题的正确结果。除此以外，还给你一个整数 k ，表示你能进行以下操作的最多次数：
>
> 每次操作中，将问题的正确答案改为 'T' 或者 'F' （也就是将 answerKey[i] 改为 'T' 或者 'F' ）。
>
> 请你返回在不超过 k 次操作的情况下，最大 连续 'T' 或者 'F' 的数目。

示例一：

```java
输入：answerKey = "TTFF", k = 2
输出：4
解释：我们可以将两个 'F' 都变为 'T' ，得到 answerKey = "TTTT" 。
总共有四个连续的 'T' 。
```

示例二：

```java
输入：answerKey = "TFFT", k = 1
输出：3
解释：我们可以将最前面的 'T' 换成 'F' ，得到 answerKey = "FFFT" 。
或者，我们可以将第二个 'T' 换成 'F' ，得到 answerKey = "TFFF" 。
两种情况下，都有三个连续的 'F' 。
```

示例三：

```java
输入：answerKey = "TTFTTFTT", k = 1
输出：5
解释：我们可以将第一个 'F' 换成 'T' ，得到 answerKey = "TTTTTFTT" 。
或者我们可以将第二个 'F' 换成 'T' ，得到 answerKey = "TTFTTTTT" 。
两种情况下，都有五个连续的 'T' 。
```

思路：

> 滑动窗口：只要求最大连续指定字符的数目时，本题和「1004. 最大连续1的个数 III」完全一致。
>
> 在指定字符的情况下，我们可以计算其最大连续数目。具体地，我们使用滑动窗口的方法，从左到右枚举右端点，维护区间中另一种字符的数量为 sum，当 sum 超过 k，我们需要让左端点右移，直到 sum≤k。移动过程中，我们记录滑动窗口的最大长度，即为指定字符的最大连续数目。
>
> 本题的答案为分别指定字符为 T 和 F时的最大连续数目的较大值。

代码：

```java
//滑动窗口：O(n),O()
public int maxConsecutiveAnswers(String answerKey, int k) {
    return Math.max(maxConsecutiveChar(answerKey, k, 'T'), maxConsecutiveChar(answerKey, k, 'F'));
}
//将字符改为c，操作最多k次，能形成的最大连续长度
public int maxConsecutiveChar(String answerKey, int k, char ch) {
    int n = answerKey.length();
    int ans = 0;
    for (int left = 0, right = 0, sum = 0; right < n; right++) {
        sum += answerKey.charAt(right) != ch ? 1 : 0;	//使用1次操作
        while (sum > k) {	
            sum -= answerKey.charAt(left++) != ch ? 1 : 0;	//恢复1次
        }
        ans = Math.max(ans, right - left + 1);
    }
    return ans;
}
```



### 2038. 如果相邻两个颜色均相同则删除当前颜色

> 总共有 n 个颜色片段排成一列，每个颜色片段要么是 'A' 要么是 'B' 。给你一个长度为 n 的字符串 colors ，其中 colors[i] 表示第 i 个颜色片段的颜色。
>
> Alice 和 Bob 在玩一个游戏，他们 轮流 从这个字符串中删除颜色。Alice 先手 。
>
> 如果一个颜色片段为 'A' 且 相邻两个颜色 都是颜色 'A' ，那么 Alice 可以删除该颜色片段。Alice 不可以 删除任何颜色 'B' 片段。
> 如果一个颜色片段为 'B' 且 相邻两个颜色 都是颜色 'B' ，那么 Bob 可以删除该颜色片段。Bob 不可以 删除任何颜色 'A' 片段。
> Alice 和 Bob 不能 从字符串两端删除颜色片段。
> 如果其中一人无法继续操作，则该玩家 输 掉游戏且另一玩家 获胜 。
>
> 假设 Alice 和 Bob 都采用最优策略，如果 Alice 获胜，请返回 true，否则 Bob 获胜，返回 false。

示例一：

```java
输入：colors = "AAABABB"
输出：true
解释：
AAABABB -> AABABB
Alice 先操作。
她删除从左数第二个 'A' ，这也是唯一一个相邻颜色片段都是 'A' 的 'A' 。

现在轮到 Bob 操作。
Bob 无法执行任何操作，因为没有相邻位置都是 'B' 的颜色片段 'B' 。
因此，Alice 获胜，返回 true 。
```

示例二：

```java
输入：colors = "AA"
输出：false
解释：
Alice 先操作。
只有 2 个 'A' 且它们都在字符串的两端，所以她无法执行任何操作。
因此，Bob 获胜，返回 false 。
```

示例三：

```java
输入：colors = "ABBBBBBBAAA"
输出：false
解释：
ABBBBBBBAAA -> ABBBBBBBAA
Alice 先操作。
她唯一的选择是删除从右数起第二个 'A' 。

ABBBBBBBAA -> ABBBBBBAA
接下来轮到 Bob 操作。
他有许多选择，他可以选择任何一个 'B' 删除。

然后轮到 Alice 操作，她无法删除任何片段。
所以 Bob 获胜，返回 false 。
```

思路：

> 贪心算法：根据题意，当 colors中有一串连续的长度为 LA 的 A时，Alice 可以删除中间的 LA-2，而不能删除两边的 2 个 A。并且 Bob删除 B的操作，不会影响 Alice删除 LA 的操作。
>
> 同理，当 colors中有一串连续的长度为 LB 时，Bob可以删除中间的 LB−2，而不能删除两边的 2 个 B。并且 Alice删除 A的操作，不会影响 Bob删除 LB 的操作。
>
> 根据这两个结论，我们可以分别计算出 Alice和 Bob的操作数。当 Alice操作数大于 Bob的操作数时，Alice获胜；否则，Bob获胜。
>

代码：

```java
public boolean winnerOfGame(String colors) {
    char cur = 'C';
    int cnt = 0;
    int[] result = {0,0};
    for(int i = 0; i < colors.length(); i++){
        char c = colors.charAt(i);
        if(c != cur){
            cnt = 1;
            cur = c;
        }else{
            cnt++;
            if(cnt >= 3){
                result[cur - 'A']++;
            }
        }
    }
    return result[0] > result[1];
}
```



## 困难



# 链表

## 简单

### 21. 合并有序列表

> 将两个升序链表合并为一个新的 **升序** 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

示例一：

```java
输入：l1 = [1,2,4], l2 = [1,3,4]
输出：[1,1,2,3,4,4]
```

示例二：

```java
输入：l1 = [], l2 = []
输出：[]
```

示例三：

```java
输入：l1 = [], l2 = [0]
输出：[0]
```

代码：

```java
//迭代
public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
    if(list1 == null && list2 == null){
        return null;
    }
    if(list1 == null){
        return list2;
    }
    if(list2 == null){
        return list1;
    }
    ListNode head = new ListNode(-1);
    ListNode cur = head;
    while(list1 != null && list2 != null){
        if(list1.val < list2.val){
            cur.next = list1;
            list1 = list1.next;
        }else{
            cur.next = list2;
            list2 = list2.next;
        }
        cur = cur.next;
    }
    if(list1 == null){
        cur.next = list2;
    }else{
        cur.next = list1;
    }
    return head.next;
}
//官方答案的迭代：O(m+n),O(1)
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    ListNode prehead = new ListNode(-1);
    ListNode prev = prehead;
    while (l1 != null && l2 != null) {
        if (l1.val <= l2.val) {
            prev.next = l1;
            l1 = l1.next;
        } else {
            prev.next = l2;
            l2 = l2.next;
        }
        prev = prev.next;
    }
    // 合并后 l1 和 l2 最多只有一个还未被合并完，我们直接将链表末尾指向未合并完的链表即可
    prev.next = l1 == null ? l2 : l1;
    return prehead.next;
}
//递归:O
public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
    if(list1 == null){
        return list2;
    }
    if(list2 == null){
        return list1;
    }
    if(list1.val < list2.val){
        list1.next = mergeTwoLists(list1.next, list2);
        return list1;
    }else{
        list2.next = mergeTwoLists(list1,list2.next);
        return list2;
    }
}
```



### 876. 链表的中间结点

> 给定一个头结点为 `head` 的非空单链表，返回链表的中间结点。
>
> 如果有两个中间结点，则返回第二个中间结点。

示例一:

```java
输入：[1,2,3,4,5]
输出：此列表中的结点 3 (序列化形式：[3,4,5])
返回的结点值为 3 。 (测评系统对该结点序列化表述是 [3,4,5])。
注意，我们返回了一个 ListNode 类型的对象 ans，这样：
ans.val = 3, ans.next.val = 4, ans.next.next.val = 5, 以及 ans.next.next.next = NULL.
```

示例二：

```java
输入：[1,2,3,4,5,6]
输出：此列表中的结点 4 (序列化形式：[4,5,6])
由于该列表有两个中间结点，值分别为 3 和 4，我们返回第二个结点。
```

思路：

> 快慢指针法（双指针）：用两个指针 `slow` 与 `fast` 一起遍历链表。`slow` 一次走一步，`fast` 一次走两步。那么当 `fast` 到达链表的末尾时，`slow` 必然位于中间。

代码：

```java
//暴力破解
public ListNode middleNode(ListNode head) {
    ListNode list = new ListNode();
    list = head;
    int count = 0;
    while(list != null){
        list = list.next;
        count++;
    }
    list = head;
    int temp = 1;
    while(temp < count / 2 +1){
        if(list.next == null){
            return list;
        }
        list = list.next;
        temp++;
    }
    return list;
}
//官方答案，单指针法:O(n),O(1)
public ListNode middleNode(ListNode head) {
    ListNode list = new ListNode();
    list = head;
    int count = 0;
    while(list != null){
        list = list.next;
        count++;
    }
    list = head;
    int temp = 0;
    while(temp < count / 2){
        list = list.next;
        temp++;
    }
    return list;
}
//数组法：O(n),O(n)
public ListNode middleNode(ListNode head) {
    ListNode[] list = new ListNode[100];
    int num = 0;
    while(head != null){
        list[num++] = head;
        head = head.next;
    }
    return list[num/2];
}
//快慢指针法：O(n),O(1)
public ListNode middleNode(ListNode head) {
    ListNode fast = head;
    ListNode slow = head;
    while(fast != null && fast.next != null){
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow;
}
```



## 中等

### [02. 两数相加](https://leetcode.cn/problems/add-two-numbers/)

> 给你两个 非空 的链表，表示两个非负的整数。它们每位数字都是按照 逆序 的方式存储的，并且每个节点只能存储 一位 数字。
>
> 请你将两个数相加，并以相同形式返回一个表示和的链表。
>
> 你可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例1：

```java
输入：l1 = [2,4,3], l2 = [5,6,4]
输出：[7,0,8]
解释：342 + 465 = 807.
```

示例2:

```java
输入：l1 = [0], l2 = [0]
输出：[0]
```

示例3:

```java
输入：l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
输出：[8,9,9,9,0,0,0,1]
```

代码：

```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
  //定义一个新联表伪指针，用来指向头指针，返回结果
  ListNode prev = new ListNode(0);
  //定义一个进位数的指针，用来存储当两数之和大于10的时候，
  int carry = 0;
  //定义一个可移动的指针，用来指向存储两个数之和的位置
  ListNode cur = prev;
  //当l1 不等于null或l2 不等于空时，就进入循环
  while(l1 != null || l2 != null){
    //如果l1 不等于null时，就取他的值，等于null时，就赋值0，保持两个链表具有相同的位数
    int x = l1 != null ? l1.val : 0;
    //如果l1 不等于null时，就取他的值，等于null时，就赋值0，保持两个链表具有相同的位数
    int y = l2 != null ? l2.val : 0;
    //将两个链表的值，进行相加，并加上进位数
    int sum = x + y + carry;
    //计算进位数
    carry = sum / 10;
    //计算两个数的和，此时排除超过10的请况（大于10，取余数）
    sum = sum % 10;
    //将求和数赋值给新链表的节点，
    cur.next = new ListNode(sum);
    //将新链表的节点后移
    cur = cur.next;
    //当链表l1不等于null的时候，将l1 的节点后移
    if(l1 != null){
      l1 = l1.next;
    }
    //当链表l2 不等于null的时候，将l2的节点后移
    if(l2 != null){
      l2 = l2.next;
    }
  }
  //如果最后两个数，相加的时候有进位数的时候，就将进位数，赋予链表的新节点。
  if(carry == 1){
    cur.next = new ListNode(1);
  }
  //返回链表的头节点
  return prev.next;
}
```



### 19. 删除链表的倒数第N个结点

> 给你一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。

示例一：

```java
输入：head = [1,2,3,4,5], n = 2
输出：[1,2,3,5]
```

示例二：

```java
输入：head = [1], n = 1
输出：[]
```

示例三：

```java
输入：head = [1,2], n = 1
输出：[1]
```

代码：

```java
//O(L)，其中 L是链表的长度,O(1)
public ListNode removeNthFromEnd(ListNode head, int n) {
    ListNode list = head;
    int count = 0;
    while(list != null){
        list = list.next;
        count++;
    }
    ListNode preHead = new ListNode(0, head);
    ListNode cur = preHead;
    int temp = 1;
    while(temp < count -n + 1){
        temp++;
        cur = cur.next;
    }
    cur.next = cur.next.next;
    return preHead.next;
}
//双指针
public ListNode removeNthFromEnd(ListNode head, int n) {
    ListNode preHead = new ListNode(0, head);
    ListNode first = head;
    ListNode second = preHead;
    for (int i = 0; i < n; i++) {
        first = first.next;
    }
    while(first != null){
        second = second.next;
        first = first.next;
    }
    second.next = second.next.next;
    return preHead.next;
}
```

### 82. 删除排序链表中的重复元素 II

> 给定一个已排序的链表的头 `head` ， *删除原始链表中所有重复数字的节点，只留下不同的数字* 。返回 *已排序的链表* 

示例一：

```java
输入：head = [1,2,3,3,4,4,5]
输出：[1,2,5]
```

示例二：

```java
输入：head = [1,1,1,2,3]
输出：[2,3]
```

思路：

>**方法一：一次遍历**
>由于给定的链表是排好序的，因此重复的元素在链表中出现的位置是连续的，因此我们只需要对链表进行一次遍历，就可以删除重复的元素。由于链表的头节点可能会被删除，因此我们需要额外使用一个哑节点（dummy node）指向链表的头节点。
>具体地，我们从指针 cur 指向链表的哑节点，随后开始对链表进行遍历。如果当前 cur.next 与 cur.next.next 对应的元素相同，那么我们就需要将 cur.next 以及所有后面拥有相同元素值的链表节点全部删除。我们记下这个元素值 x，随后不断将 cur.next 从链表中移除，直到 cur.next为空节点或者其元素值不等于 x 为止。此时，我们将链表中所有元素值为 x 的节点全部删除。
>如果当前 cur.next 与 cur.next.next对应的元素不相同，那么说明链表中只有一个元素值为 cur.next 的节点，那么我们就可以将 cur 指向 cur.next。
>当遍历完整个链表之后，我们返回链表的的哑节点的下一个节点 dummy.next即可。
>需要注意 cur.next以及 cur.next.next可能为空节点，如果不加以判断，可能会产生运行错误。

代码：

```java
//双指针：O(n),O(1)
public ListNode deleteDuplicates(ListNode head) {
    if(head == null){
        return head;
    }
    ListNode node = new ListNode(0, head);
    ListNode cur = node;
    while(cur.next != null && cur.next.next != null){
        if(cur.next.val == cur.next.next.val){
            int x = cur.next.val;
            while(cur.next != null && cur.next.val == x){
                cur.next = cur.next.next;
            }
        }else{
            cur = cur.next;
        }
    }
    return node.next;
}
```

### [138. 复制带随机指针的链表](https://leetcode.cn/problems/copy-list-with-random-pointer/)

> 给你一个长度为 n 的链表，每个节点包含一个额外增加的随机指针 random ，该指针可以指向链表中的任何节点或空节点。
>
> 构造这个链表的 深拷贝。 深拷贝应该正好由 n 个 全新 节点组成，其中每个新节点的值都设为其对应的原节点的值。新节点的 next 指针和 random 指针也都应指向复制链表中的新节点，并使原链表和复制链表中的这些指针能够表示相同的链表状态。复制链表中的指针都不应指向原链表中的节点 。
>
> 例如，如果原链表中有 X 和 Y 两个节点，其中 X.random --> Y 。那么在复制链表中对应的两个节点 x 和 y ，同样有 x.random --> y 。
>
> 返回复制链表的头节点。
>
> 用一个由 n 个节点组成的链表来表示输入/输出中的链表。每个节点用一个 [val, random_index] 表示：
>
> val：一个表示 Node.val 的整数。
> random_index：随机指针指向的节点索引（范围从 0 到 n-1）；如果不指向任何节点，则为  null 。
> 你的代码 只 接受原链表的头节点 head 作为传入参数。

示例一：

```java
输入：head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
输出：[[7,null],[13,0],[11,4],[10,2],[1,0]]
```

示例二：

```java
输入：head = [[1,1],[2,1]]
输出：[[1,1],[2,1]]
```

示例三：

```java
输入：head = [[3,null],[3,0],[3,null]]
输出：[[3,null],[3,0],[3,null]]
```

代码：

```java
// 方法一：哈希表O(n), O(n)
public static Node copyRandomList1(Node head) {
    // key 老节点
    // value 新节点
    HashMap<Node, Node> map = new HashMap<>();
    Node cur = head;
    while(cur != null){
        map.put(cur, new Node(cur.val));
        cur = cur.next;
    }
    cur = head;
    while(cur != null){
        // cur 老
        // map.get(cur) 新
        // 新.next ->  cur.next克隆节点找到
        map.get(cur).next = map.get(cur.next);
        map.get(cur).random = map.get(cur.random);
        cur = cur.next;
    }
    return map.get(head);
}
// 节点拆分	O(n), O(1)
public static Node copyRandomList2(Node head) {
    if (head == null) {
        return null;
    }
    Node cur = head;
    Node next = null;
    // 1 -> 2 -> 3 -> null
    // 1 -> 1' -> 2 -> 2' -> 3 -> 3'
    while (cur != null) {
        next = cur.next;
        cur.next = new Node(cur.val);
        cur.next.next = next;
        cur = next;
    }
    cur = head;
    Node copy = null;
    // 1 1' 2 2' 3 3'
    // 依次设置 1' 2' 3' random指针
    while (cur != null) {
        next = cur.next.next;
        copy = cur.next;
        copy.random = cur.random != null ? cur.random.next : null;
        cur = next;
    }
    Node res = head.next;
    cur = head;
    // next方向上，把新老链表分离
    while (cur != null) {
        next = cur.next.next;
        copy = cur.next;
        cur.next = next;
        copy.next = next != null ? next.next : null;
        cur = next;
    }
    return res;
}
```



## 困难



# 栈

## 简单

### [20. 有效的括号](https://leetcode.cn/problems/valid-parentheses/)

> 给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串 s ，判断字符串是否有效。
>
> 有效字符串需满足：
>
> 左括号必须用相同类型的右括号闭合。
> 左括号必须以正确的顺序闭合。
> 每个右括号都有一个对应的相同类型的左括号。

示例一：

```java
输入：s = "()"
输出：true
```

示例二：

```java
输入：s = "()[]{}"
输出：true
```

示例三：

```java
输入：s = "(]"
输出：false
```

思路：

>当我们遇到一个左括号时，我们会期望在后续的遍历中，有一个相同类型的右括号将其闭合。由于后遇到的左括号要先闭合，因此我们可以将这个左括号放入栈顶。
>
>当我们遇到一个右括号时，我们需要将一个相同类型的左括号闭合。此时，我们可以取出栈顶的左括号并判断它们是否是相同类型的括号。如果不是相同的类型，或者栈中并没有左括号，那么字符串 s 无效，返回False。为了快速判断括号的类型，我们可以使用哈希表存储每一种括号。哈希表的键为右括号，值为相同类型的左括号。
>
>在遍历结束后，如果栈中没有左括号，说明我们将字符串 s 中的所有左括号闭合，返回 True，否则返回 False。
>
>注意到有效字符串的长度一定为偶数，因此如果字符串的长度为奇数，我们可以直接返回 False，省去后续的遍历判断过程。

代码：

```java
// 时间复杂度：O(N)
public boolean isValid(String s) {
  int length = s.length();
  // 如果字符串长度为奇数则肯定存在不匹配问题，直接返回
  if(length % 2 == 1){
    return false;
  }
  // 将对应的括号存在哈希表中
  Map<Character, Character> pairs = new HashMap<Character, Character>();
  pairs.put(')', '(');
  pairs.put(']', '[');
  pairs.put('}', '{');
  // 使用栈来保存字符串中的左侧括号
  Deque<Character> stack = new LinkedList<Character>();
  for(int i = 0; i < length; i++){
    char ch = s.charAt(i);
    // 判断字符是左括号还是右括号，如果哈希表中存在，则证明是有括号，否则为左括号
    if(pairs.containsKey(ch)){
      // 如果当前字符是右括号，而栈为空或者栈顶元素与该符号不是配对符号，则返回
      if(stack.isEmpty() || stack.peek() != pairs.get(ch)){
        return false;
      }
      // 如果匹配则弹出对应的栈顶元素即对应的左括号弹出左符号栈
      stack.pop();
    }else{
      // 当前字符为左括号，保存在括号栈中
      stack.push(ch);
    }
  }
  // 如果完全匹配则括号栈应为空返回true，否则不匹配
  return stack.isEmpty();
}
```



## 中等



## 困难



# 数学

## 简单

### [9. 回文数](https://leetcode.cn/problems/palindrome-number/)

>给你一个整数 x ，如果 x 是一个回文整数，返回 true ；否则，返回 false 。
>
>回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。
>
>例如，121 是回文，而 123 不是。

示例一：

```java
输入：x = 121
输出：true
```

示例二：

```java
输入：x = -121
输出：false
解释：从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。
```

示例三：

```java
输入：x = 10
输出：false
解释：从右向左读, 为 01 。因此它不是一个回文数。
```

思路：

>通过取整和取余操作获取整数中对应的数字进行比较。
>举个例子：1221 这个数字。
>
>通过计算 1221 / 1000， 得首位1
>通过计算 1221 % 10， 可得末位 1
>进行比较
>再将 22 取出来继续比较

代码：

```java
public boolean isPalindrome(int x) {
  // 边界判断
  if(x < 0 || (x % 10 == 0 && x != 0)){
    return false;
  }
  int div = 1;
  while(x / div >= 10){
    div *= 10;
  }
  while(x > 0){
    int left = x / div;
    int right = x % 10;
    if(left != right){
      return false;
    }
    x = (x % div) / 10;
    div = div / 100;
  }
  return true;
}
```



### 868. 二进制间距

> 给定一个正整数 n，找到并返回 n 的二进制表示中两个 相邻 1 之间的 最长距离 。如果不存在两个相邻的 1，返回 0 。
>
> 如果只有 0 将两个 1 分隔开（可能不存在 0 ），则认为这两个 1 彼此 相邻 。两个 1 之间的距离是它们的二进制表示中位置的绝对差。例如，"1001" 中的两个 1 的距离为 3 。

示例一：

```java
输入：n = 22
输出：2
解释：22 的二进制是 "10110" 。
在 22 的二进制表示中，有三个 1，组成两对相邻的 1 。
第一对相邻的 1 中，两个 1 之间的距离为 2 。
第二对相邻的 1 中，两个 1 之间的距离为 1 。
答案取两个距离之中最大的，也就是 2 。
```

示例二：

```java
输入：n = 8
输出：0
解释：8 的二进制是 "1000" 。
在 8 的二进制表示中没有相邻的两个 1，所以返回 0 。
```

示例三：

```java
输入：n = 5
输出：2
解释：5 的二进制是 "101" 。
```

思路：

>记住 Java 有这样一个函数：`Integer.toBinaryString`，它的作用是将数字转成其对应的二进制字符串（例如：`22 -> "10110"`），它是你做二进制题目最后一棵稻草...
>
>思路1：数字转二进制字符串，遍历二进制字符串，每次记录上一个 1 出现的位置
>
>方法二：
>
>我们可以使用一个循环从 n 二进制表示的低位开始进行遍历，并找出所有的 1。我们用一个变量 last 记录上一个找到的 1 的位置。如果当前在第 i 位找到了 1，那么就用 i−last更新答案，再将 last更新为 i 即可。
>
>在循环的每一步中，我们可以使用位运算 n & 1 获取 n 的最低位，判断其是否为 111。在这之后，我们将 n 右移一位：n = n >> 1，这样在第 i 步时，n & 1得到的就是初始 n 的第 i 个二进制位。
>

代码：

```java
public int binaryGap(int n) {
    String binary = Integer.toBinaryString(n);
    int lastIndex = n;
    int maxGap = 0;
    for(int i = 0; i < binary.length(); i++){
        if(binary.charAt(i) == '1'){
            maxGap = Math.max(maxGap, i - lastIndex);
            lastIndex = i;
        }
    }
    return maxGap;
}
//位运算：O
public int binaryGap(int n) {
    int lastIndex = n, ans = 0;
    for(int i = 0; n != 0; i++){
        if((n & 1) == 1){
            ans = Math.max(ans, i - lastIndex);
            lastIndex = i;
        }
        n >>= 1;
    }
    return ans;
}
```



## 中等

### [7. 整数反转](https://leetcode.cn/problems/reverse-integer/)

> 给你一个 32 位的有符号整数 x ，返回将 x 中的数字部分反转后的结果。
>
> 如果反转后整数超过 32 位的有符号整数的范围 [−231,  231 − 1] ，就返回 0。
>
> 假设环境不允许存储 64 位整数（有符号或无符号）。

示例一：

```java
输入：x = 123
输出：321
```

示例二：

```java
输入：x = -123
输出：-321
```

示例三：

```java
输入：x = 120
输出：21
```

思路：

> 假设我们的环境只能存储得下 32 位的有符号整数，则其数值范围为 `[−2^31, 2^31 − 1]`，即-2147483648～2147483647
>
> 如果某个数字大于 214748364那后面就不用再判断了，肯定溢出了。
> 如果某个数字等于 214748364呢，需要要跟最大数的末尾数字比较，如果这个数字比7还大，说明溢出了。
>
> 如果某个数字**小于** `-214748364`说明溢出了
> 如果某个数字**等于** `-214748364`，还需要跟最小数的末尾比较，即看它是否小于`8`

代码：

```java
public int reverse(int x) {
  int res = 0;
  while(x != 0){
    int tmp = x % 10;
    if(res > 214748364 || (res == 214748364 && tmp > 7)){
      return 0;
    }
    if(res < -214748364 || (res == -214748364 && tmp < -8)){
      return 0;
    }
    res = res * 10 + tmp;
    x = x / 10;
  }
  return res;
}
```



### 172. 阶乘后的零

> 给定一个整数 `n` ，返回 `n!` 结果中尾随零的数量。
>
> 提示 `n! = n * (n - 1) * (n - 2) * ... * 3 * 2 * 1`

示例一：

```java
输入：n = 3
输出：0
解释：3! = 6 ，不含尾随 0
```

示例二：

```java
输入：n = 5
输出：1
解释：5! = 120 ，有一个尾随 0
```

示例三：

```java
输入：n = 0
输出：0
```

思路：

> n! 尾零的数量即为 n! 中因子 10 的个数，而 10=2×5，因此转换成求 n! 中质因子 222 的个数和质因子 555 的个数的较小值。
>
> 由于质因子 5 的个数不会大于质因子 2 的个数，我们可以仅考虑质因子 5的个数。
>
> 而 n!中质因子 5 的个数等于[1,n] 的每个数的质因子 5 的个数之和，我们可以通过遍历 [1,n] 的所有 5 的倍数求出。
>
> //优化计算
>
> ![image-20220325145625002](leecode%E5%81%9A%E9%A2%98%E7%AC%94%E8%AE%B0.assets/image-20220325145625002-16481913865311.png)
>
> ![image-20220325145707829](leecode%E5%81%9A%E9%A2%98%E7%AC%94%E8%AE%B0.assets/image-20220325145707829-16481914291842.png)

代码：

```java
public int trailingZeroes(int n) {
    int count = 0;
    for(int i = 0; i <= n; i += 5){
        int x = i;
        while(x != 0 && x % 5 == 0){
            x = x / 5;
            count++;
        }
    }
    return count;
}
//上述的简化：O(n),O()
public int trailingZeroes(int n) {
    int ans = 0;
    for (int i = 5; i <= n; i += 5) {
        for (int x = i; x % 5 == 0; x /= 5) {
            ++ans;
        }
    }
    return ans;
}
//优化计算：O(logn),O(1)
public int trailingZeroes(int n) {
    int ans = 0;
    while(n != 0){
        n = n / 5;
        ans = ans + n;
    }
    return ans;
}
```

### 398. 随机数索引

> 给你一个可能含有 重复元素 的整数数组 nums ，请你随机输出给定的目标数字 target 的索引。你可以假设给定的数字一定存在于数组中。
>
> 实现 Solution 类：
>
>     Solution(int[] nums) 用数组 nums 初始化对象。
>     int pick(int target) 从 nums 中选出一个满足 nums[i] == target 的随机索引 i 。如果存在多个有效的索引，则每个索引的返回概率应当相等。
>

示例：

```java
输入
["Solution", "pick", "pick", "pick"]
[[[1, 2, 3, 3, 3]], [3], [1], [3]]
输出
[null, 4, 0, 2]

解释
Solution solution = new Solution([1, 2, 3, 3, 3]);
solution.pick(3); // 随机返回索引 2, 3 或者 4 之一。每个索引的返回概率应该相等。
solution.pick(1); // 返回 0 。因为只有 nums[0] 等于 1 。
solution.pick(3); // 随机返回索引 2, 3 或者 4 之一。每个索引的返回概率应该相等。
```

思路：

>

代码：

```java
```



## 困难

### 479. 最大回文数乘积

> 给定一个整数 n ，返回可表示为两个 `n` 位整数乘积的 **最大回文整数**。因为答案可能非常大，所以返回它对 `1337` **取余** 。

示例一：

```java
输入：n = 2
输出：987
解释：99 x 91 = 9009, 9009 % 1337 = 987
```

示例二：

```java
输入： n = 1
输出： 9
```

思路：

> ![image-20220416150917060](leecode%E5%81%9A%E9%A2%98%E7%AC%94%E8%AE%B0.assets/image-20220416150917060-16500929584971.png)
>

代码：

```java
public int largestPalindrome(int n) {
    if(n == 1){
        return 9;
    }
    int upper = (int)Math.pow(10,n) - 1;
    int ans = 0;
    for(int left = upper;ans == 0;--left){
        long p = left;
        for(int x = left;x > 0;x /= 10){
            p = p * 10 + x % 10;
        }
        for(long x = upper;x * x >= p;--x){
            if(p % x == 0){
                ans = (int)(p % 1337);
                break;
            }
        }
    }
    return ans;
}
```



# 位运算

## 简单

### [15. 二进制中1的个数](https://leetcode.cn/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/)

> 编写一个函数，输入是一个无符号整数（以二进制串的形式），返回其二进制表达式中数字位数为 '1' 的个数（也被称为 [汉明重量](http://en.wikipedia.org/wiki/Hamming_weight)).）。

示例一：

```java
输入：n = 11 (控制台输入 00000000000000000000000000001011)
输出：3
解释：输入的二进制串 00000000000000000000000000001011 中，共有三位为 '1'。
```

示例二：

```java
输入：n = 128 (控制台输入 00000000000000000000000010000000)
输出：1
解释：输入的二进制串 00000000000000000000000010000000 中，共有一位为 '1'。
```

示例三：

```java
输入：n = 4294967293 (控制台输入 11111111111111111111111111111101，部分语言中 n = -3）
输出：31
解释：输入的二进制串 11111111111111111111111111111101 中，共有 31 位为 '1'。
```

思路：

> 方法一：循环检查二进制位：O(k), O(1)
> 当检查第i位时。我们可以让n与2^i进行与运算，当且仅当n的第i位为1时，运算结果不为0
>
> 方法二：位运算：O(logn), O(1)
> 我们可以利用这个位运算的性质加速我们的检查过程，在实际代码中，我们不断让当前的 n 与 n−1 做与运算，直到 n 变为 0 即可。因为每次运算会使得 n 的最低位的 1 被翻转，因此运算次数就等于 n 的二进制位中 
> 1 的个数。

代码：

```java
// 方法一
public int hammingWeight(int n) {
  int result = 0;
  for(int i = 0; i < 32; i++){
    if((n & (1 << i)) != 0){
      result++;
    }
  }
  return result;
}
// 方法二
public int hammingWeight(int n) {
  int result = 0;
  while(n != 0){
    n = n & (n-1);
    result++;
  }
  return result;
}
```



### 693. 交题位二进制数

> 给定一个正整数，检查它的二进制表示是否总是 0、1 交替出现：换句话说，就是二进制表示中相邻两位的数字永不相同。

示例一：

```java
输入：n = 5
输出：true
解释：5 的二进制表示是：101
```

示例二：

```java
输入：n = 7
输出：false
解释：7 的二进制表示是：111.
```

示例三：

```java
输入：n = 11
输出：false
解释：11 的二进制表示是：1011.
```

思路：

> 位运算：对输入 n 的二进制表示右移一位后，得到的数字再与 n 按位异或得到 a。当且仅当输入 n 为交替位二进制数时，a 的二进制表示全为 1（不包括前导 0）。这里进行简单证明：当 a 的某一位为 1 时，当且仅当 n 的对应位和其前一位相异。当 a 的每一位为 1 时，当且仅当 n 的所有相邻位相异，即 n 为交替位二进制数。
>
> 将 a 与 a+1 按位与，当且仅当 a 的二进制表示全为 1 时，结果为 0。这里进行简单证明：当且仅当 a 的二进制表示全为 1 时，a+1 可以进位，并将原最高位置为 0，按位与的结果为 0。否则，不会产生进位，两个最高位都为 1，相与结果不为 0
>

代码：

```java
//O(logn),O(1)
public boolean hasAlternatingBits(int n) {
    int prev = 2;
    while(n != 0){
        int cur = n % 2;
        if(cur == prev){
            return false;
        }
        prev = cur;
        n = n / 2;
    }
    return true;
}
//位运算:
public boolean hasAlternatingBits(int n) {
    int a = n ^ (n >> 1);
    return (a & (a + 1)) == 0;
}
```



## 中等



## 困难



# 字典树

## 简单



## 中等

### 386. 字典序排数

> 给你一个整数 `n` ，按字典序返回范围 `[1, n]` 内所有整数。
>
> 你必须设计一个时间复杂度为 `O(n)` 且使用 `O(1)` 额外空间的算法。

示例一：

```java
输入：n = 13
输出：[1,10,11,12,13,2,3,4,5,6,7,8,9]
```

示例二：

```java
输入：n = 2
输出：[1,2]
```

思路：

> ![image-20220418142009797](leecode%E5%81%9A%E9%A2%98%E7%AC%94%E8%AE%B0.assets/image-20220418142009797-16502628108551.png)

代码：

```java
//递归求解，递归具有额外的空间开销，O(logn)但是n取值较小，近似为O(1);O(n),O(logn)
class Solution {
    List<Integer> ans = new ArrayList<Integer>();
    public List<Integer> lexicalOrder(int n) {
        for(int i = 1; i <= 9; i++){
            dfs(i, n);
        }
        return ans;
    }

    void dfs(int cur, int limit){
        if(cur > limit){
            return;
        }
        ans.add(cur);
        for(int i = 0; i <= 9; i++){
            dfs(cur * 10 + i, limit);
        }
    }
}
//迭代求解，O(n),O(1)
public List<Integer> lexicalOrder(int n) {
    List<Integer> ans = new ArrayList<Integer>();
    int number = 1;
    for(int i = 0; i < n; i++){
        //由于ans添加完最大数后，条件会跳到else分支，最终导致除到0，再自加1得到k==1，从而无限同样的循环，因此在ans大小达到n后截断
        ans.add(number);
        if(number * 10 <= n){
            //起码可以加0，说明字典树这一支有可能继续
            number *= 10;
        }else{
            //已经不能够继续添加以“number”为真开头的数字了，那么只能退回到削减末尾的上一版开头
            while(number % 10 == 9 || number + 1 > n){
                number /= 10;
            }
            //由于此时的number开头已经遍历过了，那么我们需要继续自加1以得到同一长度下一个开头
            number += 1;
        }
    }
    return ans;
}
```



## 困难



# 动态规划

## 简单



## 中等

### [5. 最长回文子串](https://leetcode.cn/problems/longest-palindromic-substring/)

> 给你一个字符串 `s`，找到 `s` 中最长的回文子串。
>
> 如果字符串的反序与原始字符串相同，则该字符串称为回文字符串。

示例1:

```java
输入：s = "babad"
输出："bab"
解释："aba" 同样是符合题意的答案。
```

示例2:

```java
输入：s = "cbbd"
输出："bb"
```

思路：

> 对于一个子串而言，如果它是回文串，并且长度大于 22，那么将它首尾的两个字母去除之后，它仍然是个回文串。

代码：

```java
// 动态规划：O(n^2), O(n^2)
public String longestPalindrome(String s) {
  int len = s.length();
  if (len < 2) {
    return s;
  }

  int maxLen = 1;
  int begin = 0;
  // dp[i][j] 表示 s[i..j] 是否是回文串
  boolean[][] dp = new boolean[len][len];
  // 初始化：所有长度为 1 的子串都是回文串
  for (int i = 0; i < len; i++) {
    dp[i][i] = true;
  }

  char[] charArray = s.toCharArray();
  // 递推开始
  // 先枚举子串长度
  for (int L = 2; L <= len; L++) {
    // 枚举左边界，左边界的上限设置可以宽松一些
    for (int i = 0; i < len; i++) {
      // 由 L 和 i 可以确定右边界，即 j - i + 1 = L 得
      int j = L + i - 1;
      // 如果右边界越界，就可以退出当前循环
      if (j >= len) {
        break;
      }

      if (charArray[i] != charArray[j]) {
        dp[i][j] = false;
      } else {
        if (j - i < 3) {
          dp[i][j] = true;
        } else {
          dp[i][j] = dp[i + 1][j - 1];
        }
      }

      // 只要 dp[i][L] == true 成立，就表示子串 s[i..L] 是回文，此时记录回文长度和起始位置
      if (dp[i][j] && j - i + 1 > maxLen) {
        maxLen = j - i + 1;
        begin = i;
      }
    }
  }
  return s.substring(begin, begin + maxLen);
}
```

### [剑指 Offer 14- I. 剪绳子](https://leetcode.cn/problems/jian-sheng-zi-lcof/)

> 给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m-1] 。请问 k[0]*k[1]*...*k[m-1] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

示例一：

```java
输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1
```

示例二：

```java
输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36
```

思路：

>![image-20230218113722892](/Users/zhoujiajie/Library/Application Support/typora-user-images/image-20230218113722892.png)

代码：

```java
public int cuttingRope(int n) {
  int[] dp = new int[n + 1];
  for (int i = 2; i <= n; i++) {
    int curMax = 0;
    for (int j = 1; j < i; j++) {
      curMax = Math.max(curMax, Math.max(j * (i - j), j * dp[i - j]));
    }
    dp[i] = curMax;
  }
  return dp[n];
}
```



## 困难



# 贪心算法

## 简单



## 中等

### [11. 盛最多水的容器](https://leetcode.cn/problems/container-with-most-water/)

> 给定一个长度为 n 的整数数组 height 。有 n 条垂线，第 i 条线的两个端点是 (i, 0) 和 (i, height[i]) 。
>
> 找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。
>
> 返回容器可以储存的最大水量。
>
> 说明：你不能倾斜容器。

示例一：

```java
输入：[1,8,6,2,5,4,8,3,7]
输出：49 
解释：图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。
```

思路：

>双指针代表的是 可以作为容器边界的所有位置的范围。在一开始，双指针指向数组的左右边界，表示数组中所有的位置都可以作为容器的边界，因为我们还没有进行过任何尝试。在这之后，我们每次将 对应的数字较小的那个指针 往 另一个指针 的方向移动一个位置，就表示我们认为 这个指针不可能再作为容器的边界了。

代码：

```java
// 贪心算法，时间复杂度O(N), 空间复杂度O(1)
public int maxArea(int[] height) {
  int l = 0, r = height.length - 1;
  int ans = 0;
  while(l < r){
    int area = Math.min(height[l], height[r]) * (r-l);
    ans = Math.max(ans, area);
    if(height[l] < height[r]){
      l++;
    }else{
      r--;
    }
  }
  return ans;
}
```



## 困难



# 解题套路

## 二分法

> /**
>      * 范围查询规律
>           * 初始化:
>           *   int left = 0;
>                *   int right = nums.length - 1;
>                     * 循环条件
>                          *   left <= right
>                          * 右边取值
>                               *   right = mid - 1
>                               * 左边取值
>                                    *   left = mid + 1
>                                    * 查询条件
>                                         *   >= target值, 则 nums[mid] >= target时, 都减right = mid - 1
>                                         *   >  target值, 则 nums[mid] >  target时, 都减right = mid - 1
>                                         *   <= target值, 则 nums[mid] <= target时, 都加left = mid + 1
>                                         *   <  target值, 则 nums[mid] <  target时, 都加left = mid + 1
>                                         * 结果
>                                         *   求大于(含等于), 返回left
>                                         *   求小于(含等于), 返回right
>                                         * 核心思想: 要找某个值, 则查找时遇到该值时, 当前指针(例如right指针)要错过它, 让另外一个指针(left指针)跨过他(体现在left <= right中的=号), 则找到了
>                                            */

# 排序

## 简单



## 中等



## 困难

### 493.翻转对

> 给定一个数组 nums ，如果 i < j 且 nums[i] > 2*nums[j] 我们就将 (i, j) 称作一个重要翻转对。
>
> 你需要返回给定数组中的重要翻转对的数量。
>

示例一：

```java
输入: [1,3,2,3,1]
输出: 2
```

示例二：

```java
输入: [2,4,3,5,1]
输出: 3
```

思路：

> 归并排序

代码：

```java
public int reversePairs(int[] arr) {
    if (arr == null && arr.length < 2) {
        return 0;
    }
    return process(arr, 0, arr.length - 1);
}

public static int process(int[] arr, int l, int r) {
    if (l == r) {
        return 0;
    }
    int mid = l + ((r - l) >> 1);
    return process(arr, l, mid) + process(arr, mid + 1, r) + merge(arr, l, mid, r);
}

public static int merge(int[] arr, int l, int mid, int r) {
    int ans = 0;
    int win = mid + 1;
    for (int i = l; i <= mid; i++) {
        while (win <= r && (long)arr[i] > (long)arr[win] * 2) {
            win++;
        }
        ans += win - mid - 1;
    }
    int[] help = new int[r - l + 1];
    int i = 0;
    int p1 = l;
    int p2 = mid + 1;
    while (p1 <= mid && p2 <= r) {
        help[i++] = arr[p1] <= arr[p2] ? arr[p1++] : arr[p2++];
    }
    while (p1 <= mid) {
        help[i++] = arr[p1++];
    }
    while (p2 <= r) {
        help[i++] = arr[p2++];
    }
    for (i = 0; i < help.length; i++) {
        arr[l + i] = help[i];
    }
    return ans;
}
```

# 剑指 Offer

## 简单

### [03. 数组中重复的数字](https://leetcode.cn/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

> 找出数组中重复的数字。
>
> 在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

* 示例：

```java
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
```

```java
//暴力求解
class Solution {
    public int findRepeatNumber(int[] nums) {
        int n = nums.length;
        int[] arr = new int[n];
        for(int i = 0; i<nums.length;i++){
            arr[nums[i]]++;
        }
        for(int i = 0; i < arr.length;i++){
            if(arr[i]>1){
                return i;
            }
        }
        return 0;
    }
}
//HashSet
class Solution {
    public int findRepeatNumber(int[] nums) {
        Set<Integer> set_list = new HashSet<>();
        for(int num : nums){
            if(set_list.contains(num)){
                return num;
            }
            set_list.add(num);
        }
        return -1;
    }
}
```

### 05.[替换空格](https://leetcode.cn/problems/ti-huan-kong-ge-lcof/)

> 请实现一个函数，把字符串 `s` 中的每个空格替换成"%20"。

示例一：

```java
输入：s = "We are happy."
输出："We%20are%20happy."
```

思路：

>  在Java语言中，字符串都被设计成「不可变」的类型，即无法直接修改字符串的某一位字符，需要新建一个字符串实现。
> 初始化一个 list (Python) / StringBuilder (Java) ，记为 res ；
> 遍历列表 s 中的每个字符 c ：
>
>     当 c 为空格时：向 res 后添加字符串 "%20" ；
>     当 c 不为空格时：向 res 后添加字符 c ；
>
> 将列表 res 转化为字符串并返回。

代码：

```java
class Solution {
    public String replaceSpace(String s) {
        StringBuilder result = new StringBuilder();
        for(char c : s.toCharArray()){
            if(c == ' '){
                result.append("%20");
            }else{
                result.append(c);
            }
        }
        return result.toString();
    }
}
```

### [06. 从尾到头打印链表](https://leetcode.cn/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

> 输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

示例一：

```java
输入：head = [1,3,2]
输出：[2,3,1]
```

>思路：
>
>方法一：使用辅助栈
>栈的特点是后进先出，即最后压入栈的元素最先弹出。考虑到栈的这一特点，使用栈将链表元素顺序倒置。从链表的头节点开始，依次将每个节点压入栈内，然后依次弹出栈内的元素并存储到数组中。
>
>方法二：递归
>**利用递归：** 先走至链表末端，回溯时依次将节点值加入列表 ，这样就可以实现链表值的倒序输出。|
>递推阶段： 每次传入 head.next ，以 head == null（即走过链表尾部节点）为递归终止条件，此时直接返回。
>回溯阶段： 层层回溯时，将当前节点值加入列表，即tmp.add(head.val)

代码：

```java
//方法一：使用辅助栈
class Solution {
    public int[] reversePrint(ListNode head) {
        Stack<ListNode> stack = new Stack<>();
        ListNode temp = head;
        while(temp!=null){
            stack.push(temp);
            temp = temp.next;
        }
        int size = stack.size();
        int[] result = new int[size];
        for(int i = 0; i < size; i++){
            result[i] = stack.pop().val;
        }
        return result;
    }
}
//方法二：使用递归法
class Solution {
    ArrayList<Integer> list = new ArrayList<>();
    public int[] reversePrint(ListNode head) {
        recur(head);
        int size = list.size();
        int[] result = new int[size];
        for(int i =0; i < size; i++){
            result[i] = list.get(i);
        }
        return result;
    }
    public void recur(ListNode node){
        if(node == null)    return;
        recur(node.next);
        list.add(node.val);
    }
}
```

### [09. 用两个栈实现队列](https://leetcode.cn/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

> 用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

示例一：

```java
输入：
["CQueue","appendTail","deleteHead","deleteHead","deleteHead"]
[[],[3],[],[],[]]
输出：[null,null,3,-1,-1]
```

示例二：

```java
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
```

思路：

> 将一个栈当作输入栈，用于压入appendTail 传入的数据；另一个栈当作输出栈，用于 deleteHead 操作。
>
> 每次 deleteHead 时，若输出栈为空则将输入栈的全部数据依次弹出并压入输出栈，这样输出栈从栈顶往栈底的顺序就是队列从队首往队尾的顺序。
>

代码：

```java
//双栈：O(1),O(n)
class CQueue {
    //inStack用作插入，outStack用作删除
    Deque<Integer> inStack;
    Deque<Integer> outStack;

    public CQueue() {
        inStack = new ArrayDeque<Integer>();
        outStack = new ArrayDeque<Integer>();
    }
    
    public void appendTail(int value) {
        inStack.push(value);
    }
    
    public int deleteHead() {
        if(outStack.isEmpty()){
            if(inStack.isEmpty()){
                return -1;
            }
            in_out();
        }
        return outStack.pop();
        
    }

    public void in_out(){
        while(!inStack.isEmpty()){
            outStack.push(inStack.pop());
        }
    }
}
```

### [10- I. 斐波那契数列](https://leetcode.cn/problems/fei-bo-na-qi-shu-lie-lcof/)

> 写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项（即 F(N)）。斐波那契数列的定义如下：
>
> F(0) = 0,   F(1) = 1
> F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
> 斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。
>
> 答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

示例一：

```java
输入：n = 2
输出：1
```

示例二：

```java
输入：n = 5
输出：5
```

代码：

```java
//动态规划
class Solution {
    public int fib(int n) {
        if(n == 0){
            return 0;
        }
        
        int[] dp = new int[n+1];
        dp[0] = 0;
        dp[1] = 1;
        
        for(int i = 2; i <= n; i++){
            dp[i] = dp[i-1]+dp[i-2];
            dp[i] %= 1000000007;
        }

        return dp[n];
    }
}
```

### [10- II. 青蛙跳台阶问题](https://leetcode.cn/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/)

> 一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 n 级的台阶总共有多少种跳法。
>
> 答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

示例一：

```java
输入：n = 2
输出：2
```

示例二：

```java
输入：n = 7
输出：21
```

示例三：

```java
输入：n = 0
输出：1
```

思路：

> 此类求 *多少种可能性* 的题目一般都有 **递推性质** ，即 f(n)*f*(*n*) 和 f(n-1)*f*(*n*−1)…f(1)*f*(1) 之间是有联系的。
>
> 设跳上 n级台阶有 f(n) 种跳法。在所有跳法中，青蛙的最后一步只有两种情况： **跳上 1 级或 2 级台阶**
>
> 1. **当为 1 级台阶：** 剩 n-1个台阶，此情况共有 f(n-1) 种跳法；
> 2. **当为 2级台阶：** 剩 n-2个台阶，此情况共有 f(n-2)种跳法。
>
> ![image-20221117154521258](leecode%E5%81%9A%E9%A2%98%E7%AC%94%E8%AE%B0.assets/image-20221117154521258.png)

代码：

```java
class Solution {
    public int numWays(int n) {
        if(n == 0){
            return 1;
        }
        int[] dp = new int[n+1];
        dp[0] = 1;
        dp[1] = 1;
        for(int i = 2; i <= n; i++){
            dp[i] = dp[i-1]+dp[i-2];
            dp[i] %= 1000000007;
        }
        return dp[n];
    }
}
```

### [11. 旋转数组的最小数字](https://leetcode.cn/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)

> 把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。
>
> 给你一个可能存在 重复 元素值的数组 numbers ，它原来是一个升序排列的数组，并按上述情形进行了一次旋转。请返回旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一次旋转，该数组的最小值为 1。  
>
> 注意，数组 [a[0], a[1], a[2], ..., a[n-1]] 旋转一次 的结果为数组 [a[n-1], a[0], a[1], a[2], ..., a[n-2]] 。

示例一：

```java
输入：numbers = [3,4,5,1,2]
输出：1
```

示例二：

```java
输入：numbers = [2,2,2,0,1]
输出：0
```

思路：

>我们考虑数组中的最后一个元素 x：在最小值右侧的元素，它们的值一定都小于等于 x；而在最小值左侧的元素，它们的值一定都大于等于 x。因此，我们可以根据这一条性质，通过二分查找的方法找出最小值。
>在二分查找的每一步中，左边界为low，右边界为high，区间的中点为 pivot，最小值就在该区间内。我们将中轴元素numbers[pivot] 与右边界元素numbers[high] 进行比较，可能会有以下的三种情况：
>**第一种情况是 numbers[pivot]<numbers[high]**。如下图所示，这说明numbers[pivot] 是最小值右侧的元素，因此我们可以忽略二分查找区间的右半部分。
>**第二种情况是numbers[pivot]>numbers[high]**。如下图所示，这说明numbers[pivot] 是最小值左侧的元素，因此我们可以忽略二分查找区间的左半部分。
>**第三种情况是numbers[pivot]==numbers[high]**。如下图所示，由于重复元素的存在，我们并不能确定 numbers[pivot] 究竟在最小值的左侧还是右侧，因此我们不能莽撞地忽略某一部分的元素。我们唯一可以知道的是，由于它们的值相同，所以无论 numbers[high] 是不是最小值，都有一个它的「替代品」numbers[pivot]，因此我们可以忽略二分查找区间的右端点。

代码：

```java
//暴力求解，求数组最小值
class Solution {
    public int minArray(int[] numbers) {
        int min = numbers[0];
        for(int i = 0; i < numbers.length; i++){
            if(numbers[i] < min){
                min = numbers[i];
            }
        }
        return min;
    }
}
//二分法
class Solution {
    public int minArray(int[] numbers) {
        int left = 0, right = numbers.length-1;
        while(left < right){
            int mid = left + (right - left) / 2;
            if(numbers[mid] > numbers[right]){
                //证明mid前面一定是有序的，最小值在mid后面，可以缩小查找范围，放弃前半部分
                left = mid + 1;
            }else if(numbers[mid] < numbers[right]){
                // mid后半部分一定是有序的，但是不确定mid是否是最小值
                right = mid;
            }else{
                // mid值与right值相等时，并不能确定分界点在mid前还是mid后，暴力从右到左遍历，缩小范围
                right = right - 1;
            }
        }
        return numbers[left];
    }
}
```

### [15. 二进制中1的个数](https://leetcode.cn/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/)

> 编写一个函数，输入是一个无符号整数（以二进制串的形式），返回其二进制表达式中数字位数为 '1' 的个数（也被称为 [汉明重量](http://en.wikipedia.org/wiki/Hamming_weight)).）。

示例一：

```java
输入：n = 11 (控制台输入 00000000000000000000000000001011)
输出：3
解释：输入的二进制串 00000000000000000000000000001011 中，共有三位为 '1'。
```

示例二：

```java
输入：n = 128 (控制台输入 00000000000000000000000010000000)
输出：1
解释：输入的二进制串 00000000000000000000000010000000 中，共有一位为 '1'。
```

示例三：

```java
输入：n = 4294967293 (控制台输入 11111111111111111111111111111101，部分语言中 n = -3）
输出：31
解释：输入的二进制串 11111111111111111111111111111101 中，共有 31 位为 '1'。
```

思路：

> 方法一：循环检查二进制位：O(k), O(1)
> 当检查第i位时。我们可以让n与2^i进行与运算，当且仅当n的第i位为1时，运算结果不为0
>
> 方法二：位运算：O(logn), O(1)
> 我们可以利用这个位运算的性质加速我们的检查过程，在实际代码中，我们不断让当前的 n 与 n−1 做与运算，直到 n 变为 0 即可。因为每次运算会使得 n 的最低位的 1 被翻转，因此运算次数就等于 n 的二进制位中 
> 1 的个数。

代码：

```java
// 方法一
public int hammingWeight(int n) {
  int result = 0;
  for(int i = 0; i < 32; i++){
    if((n & (1 << i)) != 0){
      result++;
    }
  }
  return result;
}
// 方法二
public int hammingWeight(int n) {
  int result = 0;
  while(n != 0){
    n = n & (n-1);
    result++;
  }
  return result;
}
```

### [17. 打印从1到最大的n位数](https://leetcode.cn/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/)

> 输入数字 `n`，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。

示例一：

```java
输入: n = 1
输出: [1,2,3,4,5,6,7,8,9]
```

代码：

```java
public int[] printNumbers(int n) {
  int end = (int) Math.pow(10, n) - 1;
  int[] ans = new int[end];
  for(int i = 1; i < Math.pow(10, n); i++){
    ans[i-1] = i;
  }
  return ans;
}
```

### [18. 删除链表的节点](https://leetcode.cn/problems/shan-chu-lian-biao-de-jie-dian-lcof/)

> 给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。
>
> 返回删除后的链表的头节点。

示例一：

```java
输入: head = [4,5,1,9], val = 5
输出: [4,1,9]
解释: 给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.
```

示例二：

```java
输入: head = [4,5,1,9], val = 1
输出: [4,5,9]
解释: 给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.
```

代码：

```java
// 单指针
class Solution {
    public ListNode deleteNode(ListNode head, int val) {
        ListNode cur = head;
        if(head.val == val){
            head = head.next;
        }
        while(cur.next != null){
            if(cur.next.val == val){
                cur.next = cur.next.next;
            }else{
                cur = cur.next;
            }
        }
        return head;
    }
}
// 双指针：O(N),O(1)
class Solution {
    public ListNode deleteNode(ListNode head, int val) {
        if(head.val == val) return head.next;
        ListNode pre = head, cur = head.next;
        while(cur != null && cur.val != val){
            pre = cur;
            cur = cur.next;
        }
        if(cur != null){
            pre.next = cur.next;
        }
        return head;
    }
}
```



### [21. 调整数组顺序使奇数位于偶数前面](https://leetcode.cn/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/)

> 输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数在数组的前半部分，所有偶数在数组的后半部分。

示例一：

```java
输入：nums = [1,2,3,4]
输出：[1,3,2,4] 
注：[3,1,2,4] 也是正确的答案之一。
```

思路：

> 双指针：
>
> 考虑定义双指针 i, j分列数组左右两端，循环执行：
>
> 1. 指针 i从左向右寻找偶数；
> 2. 指针 j从右向左寻找奇数；
> 3. 将 偶数 nums[i] 和 奇数 nums[j] 交换
>
> 可始终保证： 指针 i左边都是奇数，指针 j 右边都是偶数 

代码：

```java
// 双端队列
class Solution {
    public int[] exchange(int[] nums) {
        Deque<Integer> deque = new ArrayDeque<>();
        for(int num : nums){
            if(num % 2 == 0){
                deque.offer(num);
            }else{
                deque.addFirst(num);
            }
        }
        int[] res = new int[nums.length];
        for(int i = 0; i < nums.length; i++){
            res[i] = deque.poll();
        }
        return res;
    }
}
// 双指针:O(n),O(1)
class Solution {
    public int[] exchange(int[] nums) {
        int i = 0, j = nums.length - 1;
        while(i < j){
            while(i < j && nums[i] % 2 == 1){
                i++;
            }
            while(i < j && nums[j] % 2 == 0){
                j--;
            }
            int temp = nums[i];
            nums[i] = nums[j];
            nums[j] = temp;
        }
        return nums;
    }
}
```



### [22. 链表中倒数第k个节点](https://leetcode.cn/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)

>输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。
>
>例如，一个链表有 6 个节点，从头节点开始，它们的值依次是 1、2、3、4、5、6。这个链表的倒数第 3 个节点是值为 4 的节点。

示例一：

```java
给定一个链表: 1->2->3->4->5, 和 k = 2.
返回链表 4->5.
```

代码：

```java
// 双指针：O(N),O(1)
class Solution {
    public ListNode getKthFromEnd(ListNode head, int k) {
        int temp = 1;
        ListNode cur = head, pre = head;
        while(temp < k){
            cur = cur.next;
            temp++;
        }
        while(cur.next != null){
            pre = pre.next;
            cur = cur.next;
        }
        return pre;
    }
}
// 大佬代码
class Solution {
    public ListNode getKthFromEnd(ListNode head, int k) {
        ListNode pre = head, cur = head;
        for(int i =0; i < k; i++){
            cur = cur.next;
        }
        while(cur != null){
            pre = pre.next;
            cur = cur.next;
        }
        return pre;
    }
}
```



### [24. 反转链表](https://leetcode.cn/problems/fan-zhuan-lian-biao-lcof/)

> 定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

示例一：

```java
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```

思路：

> 方法一：迭代O(n), O(1)
> 在遍历链表时，将当前节点的 next 指针改为指向前一个节点。由于节点没有引用其前一个节点，因此必须事先存储其前一个节点。在更改引用之前，还需要存储后一个节点。最后返回新的头引用。
>
> 方法二：递归O(n), O(n)

代码：

```java
//方法一
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode pre = null;
        ListNode cur = head;
        while(cur != null){
            ListNode next = cur.next;
            cur.next = pre;
            pre = cur;
            cur = next;
        }
        return pre;
    }
}
//方法二
class Solution {
    public ListNode reverseList(ListNode head) {
        if(head == null || head.next == null){
            return head;
        }
        ListNode newHead = reverseList(head.next);
        head.next.next = head;
        head.next = null;
        return newHead;
    }
}
```

### [25. 合并两个排序的链表](https://leetcode.cn/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/)

>输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

示例一：

```java
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

代码：

```java
// 双指针
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode head = new ListNode(0), cur = head;
        while(l1 != null && l2 != null){
            if(l1.val < l2.val){
                cur.next = l1;
                l1 = l1.next;
            }else{
                cur.next = l2;
                l2 = l2.next;
            }
            cur = cur.next;
        }
        if(l1 != null){
            cur.next = l1;
            l1 = l1.next;
        }
        if(l2 != null){
            cur.next = l2;
            l2 = l2.next;
        }
        return head.next;
    }
}
```



### [27. 二叉树的镜像](https://leetcode.cn/problems/er-cha-shu-de-jing-xiang-lcof/)

> 请完成一个函数，输入一个二叉树，该函数输出它的镜像。

示例一：

```java
输入：root = [4,2,7,1,3,6,9]
输出：[4,7,2,9,6,3,1]
```

代码：

```java
// 递归：O(N)
class Solution {
    public TreeNode mirrorTree(TreeNode root) {
        if(root == null)    return null;
        // 初始化节点tmp ，用于暂存root 的左子节点
        TreeNode temp = root.left;
        // 开启递归右子节点 mirrorTree(root.right)，并将返回值作为root的左子节点
        root.left = mirrorTree(root.right);
        // 开启递归左子节点mirrorTree(tmp) ，并将返回值作为root 的右子节点
        root.right = mirrorTree(temp);
        return root;
    }
}
// 使用辅助栈：O(n)
class Solution {
    public TreeNode mirrorTree(TreeNode root) {
        // 当root为空时，直接返回null
        if(root == null)     return null;
        // 利用栈（或队列）遍历树的所有节点node, 并交换每个node的左 / 右子节点
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        while(!stack.isEmpty()){
            TreeNode node = stack.pop();
            // 将node的左右子树入栈
            if(node.left != null)   stack.push(node.left);
            if(node.right != null)  stack.push(node.right);
            // 交换node的左右节点
            TreeNode temp = node.left;
            node.left = node.right;
            node.right = temp;
        }
        return root;
    }
}
```

### [28. 对称的二叉树](https://leetcode.cn/problems/dui-cheng-de-er-cha-shu-lcof/)

> 请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

示例一：

```java
输入：root = [1,2,2,3,4,4,3]
输出：true
```

示例二：

```java
输入：root = [1,2,2,null,3,null,3]
输出：false
```

代码：

```java
// 递归：O(n)
class Solution {
    public boolean isSymmetric(TreeNode root) {
        // 若根节点root为空，则直接返回true
        if(root == null)    return true;
        return recur(root.left, root.right);
    }
    public boolean recur(TreeNode A, TreeNode B){
        // 当L和R同时越过叶节点： 此树从顶至底的节点都对称，因此返回true
        if(A== null && B == null)   return true;
        // 当L或R中只有一个越过叶节点或当节点L值不等于节点R的值： 此树不对称，因此返回false
        if(A == null || B == null || A.val != B.val)    return false;
        // 判断两节点L.left和R.right 是否对称, 判断两节点L.right和R.left是否对称
        return recur(A.left, B.right) && recur(A.right, B.left);
    }
}
```

### [29. 顺时针打印矩阵](https://leetcode.cn/problems/shun-shi-zhen-da-yin-ju-zhen-lcof/)

> 输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

示例一：

```java
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]
```

示例二：

```java
输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]
```

思路：

> 方法一：模拟 O(mn), O(mn)
> 初始位置是矩阵的左上角，初始方向是向右，当路径超出界限或者进入之前访问过的位置时，顺时针旋转，进入下一个方向。判断路径是否进入之前访问过的位置需要使用一个与输入矩阵大小相同的辅助矩阵 visited，其中的每个元素表示该位置是否被访问过。当一个元素被访问时，将 visited 中的对应位置的元素设为已访问。如何判断路径是否结束？由于矩阵中的每个元素都被访问一次，因此路径的长度即为矩阵中的元素数量，当路径的长度达到矩阵中的元素数量时即为完整路径，将该路径返回。
>
> 方法二：按层模拟	O(mn), O(1)
> 对于每层，从左上方开始以顺时针的顺序遍历所有元素。假设当前层的左上角位于 (top,left)，右下角位于 (bottom,right)，按照如下顺序遍历当前层的元素。
>
> 1. 从左到右遍历上侧元素，依次为 (top,left)到 (top,right)
> 2. 从上到下遍历右侧元素，依次为 (top+1,right) 到 (bottom,right)
> 3. 如果 left<right 且 top<bottom，则从右到左遍历下侧元素，依次为 (bottom,right−1) 到 (bottom,left+1)，以及从下到上遍历左侧元素，依次为 (bottom,left) 到 (top+1,left)。
>
> 遍历完当前层的元素之后，将 left 和 top 分别增加 1，将 right 和 bottom 分别减少 1，进入下一层继续遍历，直到遍历完所有元素为止。

代码：

```java
// 方法一：模拟
public int[] spiralOrder(int[][] matrix) {
  if(matrix == null || matrix.length == 0 || matrix[0].length == 0){
    return new int[0];
  }
  int rows = matrix.length, columns = matrix[0].length;
  boolean[][] visited = new boolean[rows][columns];
  int total = rows * columns;
  int[] res = new int[total];
  int row = 0, column = 0;
  int[][] directions = new int[][]{{0,1},{1,0},{0,-1},{-1,0}};
  int directionIndex = 0;
  for(int i = 0; i < total; i++){
    res[i] = matrix[row][column];
    visited[row][column] = true;
    int nextRow = row + directions[directionIndex][0], nextColumn = column + directions[directionIndex][1];
    if(nextRow < 0 || nextRow >= rows || nextColumn < 0 || nextColumn >= columns || visited[nextRow][nextColumn] == true){
      directionIndex = (directionIndex + 1) % 4;
    }
    row = row + directions[directionIndex][0];
    column = column + directions[directionIndex][1];
  }
  return res;
}
// 方法二：按层模拟
public int[] spiralOrder(int[][] matrix) {
  if(matrix == null || matrix.length == 0 || matrix[0].length == 0){
    return new int[0];
  }
  int rows = matrix.length, columns = matrix[0].length;
  int index = 0;
  int[] res = new int[rows * columns];
  int left = 0, right = columns -1, top = 0, bottom = rows - 1;
  while(left <= right && top <= bottom){
    for(int column = left; column <= right; column++){
      res[index++] = matrix[top][column];
    }
    for(int row = top + 1; row <= bottom; row++){
      res[index++] = matrix[row][right];
    }
    if(left < right && top < bottom){
      for(int column = right - 1; column > left; column--){
        res[index++] = matrix[bottom][column];
      }
      for(int row = bottom; row > top; row--){
        res[index++] = matrix[row][left];
      }
    }
    left++;
    right--;
    top++;
    bottom--;
  }
  return res;
}
```



### [30. 包含min函数的栈](https://leetcode.cn/problems/bao-han-minhan-shu-de-zhan-lcof/)

> 定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

示例一：

```java
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.
```

代码：

```java
class MinStack {

    Stack<Integer> data, min;
    /** initialize your data structure here. */
    public MinStack() {
        // 数据栈，存放数据
        data = new Stack<Integer>();
        // 辅助站，存放当前最小值
        min = new Stack<Integer>();
    }
    
    public void push(int x) {
        data.push(x);
        // 如果当前添加的元素为最小值，则压入辅助栈中
        if(min.isEmpty() || min.peek() >= x){
            min.push(x);
        }
    }
    
    public void pop() {
        // 保证数据栈与辅助栈的一致性，Stack中存放的int类型为Integer，所以使用equals替代==
        if(data.pop().equals(min.peek())){
            min.pop();
        }
    }
    
    public int top() {
        return data.peek();
    }
    
    public int min() {
        return min.peek();
    }
}
```

### [31. 栈的压入、弹出序列](https://leetcode.cn/problems/zhan-de-ya-ru-dan-chu-xu-lie-lcof/)

> 输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如，序列 {1,2,3,4,5} 是某栈的压栈序列，序列 {4,5,3,2,1} 是该压栈序列对应的一个弹出序列，但 {4,3,5,1,2} 就不可能是该压栈序列的弹出序列。

示例一：

```java
输入：pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
输出：true
解释：我们可以按以下顺序执行：
push(1), push(2), push(3), push(4), pop() -> 4,
push(5), pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1
```

示例二：

```java
输入：pushed = [1,2,3,4,5], popped = [4,3,5,1,2]
输出：false
解释：1 不能在 2 之前弹出。
```

思路：

> 借用一个辅助栈stacj ，**模拟** 压入 / 弹出操作的排列。根据是否模拟成功，即可得到结果。
>
> 入栈操作： 按照压栈序列的顺序执行。
> 出栈操作： 每次入栈后，循环判断 “栈顶元素 = 弹出序列的当前元素” 是否成立，将符合弹出序列顺序的栈顶元素全部弹出

代码：

```java
// 模拟：O(n), O(n)
public boolean validateStackSequences(int[] pushed, int[] popped) {
  Deque<Integer> stack = new ArrayDeque<Integer>();
  int i = 0;
  for(int num : pushed){
    stack.push(num);
    while(!stack.isEmpty() && stack.peek() == popped[i]){
      stack.pop();
      i++;
    }
  }
  return stack.isEmpty();
}
```



### [32 - II. 从上到下打印二叉树 II](https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/)

> 从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。

示例：

```java
输入：[3,9,20,null,null,15,7]
输出：[
  [3],
  [9,20],
  [15,7]
]
```

代码：

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if(root == null)    return res;
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while(!queue.isEmpty()){
            // 列表存放当前层的节点值
            List<Integer> list = new ArrayList<>();
            // cur的值就是当前层有几个节点
            int cur = queue.size();
            // 对该层节点进行遍历，存放到该层的列表中
            for(int i = 0; i < cur; i++){
                TreeNode node = queue.poll();
                // 将节点值存入到列表中
                list.add(node.val);
                // 将该节点的左右孩子加入到队列中
                if(node.left != null)   queue.offer(node.left);
                if(node.right != null)   queue.offer(node.right);
            }
            // 将该层的列表加入到总列表中
            res.add(list);
        }
        return res;
    }
}
```

### [33. 二叉搜索树的后序遍历序列](https://leetcode.cn/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/)

> 输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 `true`，否则返回 `false`。假设输入的数组的任意两个数字都互不相同。

示例一：

```java
输入: [1,6,3,2,5]
输出: false
```

示例二：

```java
输入: [1,3,2,6,5]
输出: true
```

思路：

> **方法一：递归分治	O(N^2), O(N)**
> **终止条件：** 当 i≥j ，说明此子树节点数量 ≤1 ，无需判别正确性，因此直接返回 true 
> **递推工作：**
>
> 	1. **划分左右子树：** 遍历后序遍历的 [i,j] 区间元素，寻找 第一个大于根节点 的节点，索引记为 m 。此时，可划分出左子树区间 
> 	[i,m−1] 、右子树区间 [m,j−1] 、根节点索引 j 。
> 	2. **判断是否为二叉搜索树：**
> 	* 左子树区间 [i,m−1] 内的所有节点都应 < postorder[j] 。而第 1.划分左右子树 步骤已经保证左子树区间的正确性，因此只需要判断右子树区间即可。
> 	* 右子树区间 [m,j−1] 内的所有节点都应 < postorder[j] 。实现方式为遍历，当遇到 ≤postorder[j] 的节点则跳出；则可通过 p=j 判断是否为二叉搜索树。
>
> **返回值：** 所有子树都需正确才可判定正确，因此使用 **与逻辑符** && 连接
>
>      1. **p = j：**判断 **此树** 是否正确。
>      1. **recur(i, m-1)：** 判断 **此树的左子树** 是否正确
>      1. **recur(m, j-1)：** 判断 **此树的右子树** 是否正确

代码：

```java
// 递归分治
public boolean verifyPostorder(int[] postorder) {
  return recur(postorder,0,postorder.length-1);
}

boolean recur(int[] postorder, int i, int j){
  // 说明子树节点数量小于等于1，直接返回true
  if(i >= j)  return true;
  // 寻找左子树
  int p = i;
  // 左子树所有节点都应小于根节点
  while(postorder[p] < postorder[j]){
    p++;
  }
  int m = p;
  // 右子树所有节点都应大于根节点，遇到小于等于根节点的值则跳出
  while(postorder[p] > postorder[j]){
    p++;
  }
  // 只有当p=j时能保证该树为二叉搜索树
  return p==j && recur(postorder,i, m-1) && recur(postorder, m, j-1);
}
```

### [39. 数组中出现次数超过一半的数字](https://leetcode.cn/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/)

> 数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。
>
> 你可以假设数组是非空的，并且给定的数组总是存在多数元素。

示例一：

```java
输入: [1, 2, 3, 2, 2, 2, 5, 4, 2]
输出: 2
```

代码：

```java
// 哈希表：O(N), O(N)
public int majorityElement(int[] nums) {
  int ans = 0;
  int length = nums.length;
  Map<Integer, Integer> map = new HashMap<>();
  for(int num : nums){
    if(map.containsKey(num)){
      map.put(num, map.get(num) + 1);
    }else{
      map.put(num, 1);
    }
    if(map.get(num) > length / 2){
      ans = num;
      break;
    }
  }
  return ans;
}
// 排序：O(NlogN), O(logN)
public int majorityElement(int[] nums) {
  Arrays.sort(nums);
  return nums[nums.length / 2];
}
```



### [42. 连续子数组的最大和](https://leetcode.cn/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/)

> 输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。
>
> 要求时间复杂度为O(n)。

示例一：

```java
输入: nums = [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```

代码：

```java
// 动态规划
class Solution {
    public int maxSubArray(int[] nums) {
        int res = nums[0];
        for(int i = 1; i < nums.length; i++){
            // 当dp[i−1] > 0 时：执行dp[i]=dp[i−1]+nums[i], 当 dp[i−1]≤0 时：执行dp[i]=nums[i]
            nums[i] += Math.max(nums[i-1], 0);
            res = Math.max(nums[i], res);
        }
        return res;
    }
}
```



### [ 50. 第一个只出现一次的字符](https://leetcode.cn/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/)

> 在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

示例一：

```java
输入：s = "abaccdeff"
输出：'b'
```

示例二：

```java
输入：s = "" 
输出：' '
```

代码：

```java
// 使用哈希表，两次遍历，时间复杂度O(n),
class Solution {
    public char firstUniqChar(String s) {
        HashMap<Character, Boolean> res = new HashMap<Character, Boolean>();
        for(char c : s.toCharArray()){
            // 如果第一次放入，则对应的value值为true，一旦多次放入，value值被false覆盖
            res.put(c,!res.containsKey(c));
        }
        for(char c : s.toCharArray()){
            // 找到value值为true的，证明该值只加入到哈希表中一次，即只有一个
            if(res.get(c)){
                return c;
            }
        }
        return ' ';
    }
}
// 使用哈希表存储索引
class Solution {
    public char firstUniqChar(String s) {
        Map<Character, Integer> position = new HashMap<Character, Integer>();
        int n = s.length();
        for (int i = 0; i < n; ++i) {
            char ch = s.charAt(i);
            // 如果该字符出现多次，对应值为-1
            if (position.containsKey(ch)) {
                position.put(ch, -1);
            } else {
                // 如果第一次出现则对应值为对应的索引值
                position.put(ch, i);
            }
        }
        int first = n;
        // 遍历哈希映射中的所有值
        for (Map.Entry<Character, Integer> entry : position.entrySet()) {
            int pos = entry.getValue();
            // 找到不为-1的最小值
            if (pos != -1 && pos < first) {
                first = pos;
            }
        }
        // 如果哈希映射中的所有值均为−1，就返回空格
        return first == n ? ' ' : s.charAt(first);
    }
}
```



### [52. 两个链表的第一个公共节点](https://leetcode.cn/problems/liang-ge-lian-biao-de-di-yi-ge-gong-gong-jie-dian-lcof/)

> 输入两个链表，找出它们的第一个公共节点。

示例一：

```java
输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
输出：Reference of the node with value = 8
输入解释：相交节点的值为 8 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。
```

示例二：

```java
输入：intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
输出：Reference of the node with value = 2
输入解释：相交节点的值为 2 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [0,9,1,2,4]，链表 B 为 [3,2,4]。在 A 中，相交节点前有 3 个节点；在 B 中，相交节点前有 1 个节点。
```

思路：

>方法一：哈希表
>判断两个链表是否相交，可以使用哈希集合存储链表节点。
>首先遍历链表headA，并将链表headA 中的每个节点加入哈希集合中。然后遍历链表headB，对于遍历到的每个节点，判断该节点是否在哈希集合中：
>如果当前节点不在哈希集合中，则继续遍历下一个节点；
>如果当前节点在哈希集合中，则后面的节点都在哈希集合中，即从当前节点开始的所有节点都是两个链表的公共节点，因此在链表 headB 中遍历到的第一个在哈希集合中的节点就是两个链表的第一个公共节点，返回该节点
>
>方法二：双指针
>使用双指针的方法，可以将空间复杂度降至O(1)。
>只有当链表headA 和headB 都不为空时，两个链表才可能相交。因此首先判断链表headA 和BheadB 是否为空，如果其中至少有一个链表为空，则两个链表一定不相交，返回null。
>当链表headA 和headB 都不为空时，创建两个指针pA 和 pB，初始时分别指向两个链表的头节点headA 和headB，然后将两个指针依次遍历两个链表的每个节点。具体做法如下：
>每步操作需要同时更新指针pA和pB。
>如果指针pA不为空，则将指针pA移到下一个节点；如果指针pB不为空，则将指针pB移到下一个节点。
>如果指针pA为空，则将指针pA移到链表headB的头节点；如果指针pB为空，则将指针pB移到链表headA的头节点。
>当指针pA和pB指向同一个节点或者都为空时，返回它们指向的节点或者null
>
>双指针证明：
>![image-20221130212812129](leecode%E5%81%9A%E9%A2%98%E7%AC%94%E8%AE%B0.assets/image-20221130212812129.png)
>
>![image-20221130212832921](leecode%E5%81%9A%E9%A2%98%E7%AC%94%E8%AE%B0.assets/image-20221130212832921.png)

代码：

```java
// 哈希表：O(m+n), O(m)
class Solution {
    ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        Set<ListNode> visited = new HashSet<>();
        ListNode temp = headA;
        while(temp != null){
            visited.add(temp);
            temp = temp.next;
        }
        temp = headB;
        while(temp != null){
            if(visited.contains(temp)){
                return temp;
            }
            temp = temp.next;
        }
        return null;
    }
}
// 双指针：O(m+n), O(1)
class Solution {
    ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if(headA == null || headB == null){
            return null;
        }

        ListNode pA = headA, pB = headB;
        while(pA != pB){
            pA = pA == null ? headB : pA.next;
            pB = pB == null ? headA : pB.next;
        }
        return pA;
    }
}
```



### [53 - I. 在排序数组中查找数字 I](https://leetcode.cn/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/)

> 统计一个数字在排序数组中出现的次数。

示例一：

```java
输入: nums = [5,7,7,8,8,10], target = 8
输出: 2
```

示例二：

```java
输入: nums = [5,7,7,8,8,10], target = 6
输出: 0
```

代码：

```java
// 暴力美学
class Solution {
    public int search(int[] nums, int target) {
        int res = 0;
        for(int i =0; i < nums.length;i++){
            if(nums[i] == target){
                res++;
            }
        }
        return res;
    }
}
// 二分查找
class Solution {
    public int search(int[] nums, int target) {
        // 搜索右边界
        int left = 0, right = nums.length - 1;
        while(left <= right){
            int mid = left + (right - left) / 2;
            if(nums[mid] <= target){
                left = mid + 1;
            }else{
                right = mid - 1;
            }
        }
        // 右边界
        int res_right = left;
        // 此时right的指针应该指向右边界的左侧一个，如果此时不等于target，则数组中无target
        if(right >= 0 && nums[right] != target)
            return 0;
        // 搜索左边界
        left = 0;
        right = nums.length - 1;
        while(left <= right){
            int mid = left + (right - left) / 2;
            if(nums[mid] < target){
                left = mid + 1;
            }else{
                right = mid - 1;
            }
        }
        // 左边界
        int res_left = right;
        // 左边界为target左侧的值，右边界为target右侧的值，因此是右边界-左边界 - 1
        return res_right - res_left - 1;
    }
}
// 二分查找右边界代码封装，简化代码
class Solution {
    public int search(int[] nums, int target) {
        // 此时left为target的第一个值
        int left = helper(nums, target - 1);
        // 此时right为target的右侧第一个值
        int right = helper(nums, target);
        return right - left;
    }
    public int helper(int[] nums, int target){
        int left = 0, right = nums.length - 1;
        while(left <= right){
            int mid = left + (right - left) / 2;
            if(nums[mid] > target){
                right = mid - 1;
            }else{
                left = mid + 1;
            }
        }
        return left;
    }
}
```

### [53 - II. 0～n-1中缺失的数字](https://leetcode.cn/problems/que-shi-de-shu-zi-lcof/)

>一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。

示例一：

```java
输入: [0,1,3]
输出: 2
```

示例二：

```java
输入: [0,1,2,3,4,5,6,7,9]
输出: 8
```

代码：

```java
// 二分法
class Solution {
    public int missingNumber(int[] nums) {
        int left = 0, right = nums.length - 1;
        while(left <= right){
            int mid = left + (right - left) / 2;
            if(nums[mid] == mid){
                left = mid + 1;
            }else{
                right = mid - 1;
            }
        }
        return left;
    }
}
// 哈希集合
class Solution {
    public int missingNumber(int[] nums) {
        Set<Integer> res = new HashSet<Integer>();
        //将数组中所有值加入到集合中
        for(int i = 0; i < nums.length; i++){
            res.add(nums[i]);
        }
        int missing = -1;
        // 从0-nums.length开始遍历
        for(int i = 0; i <= nums.length;i++){
            // 如果集合中不包含i值时，直接返回
            if(!res.contains(i)){
                missing = i;
                break;
            }
        }
        return missing;
    }
}
// 直接遍历，暴力美学
class Solution {
    public int missingNumber(int[] nums) {
        for(int i =0; i < nums.length; i++){
            if(nums[i] != i){
                return i;
            }
        }
        // 如果数组中的值与索引一一对应，则缺少nums.length这个值
        return nums.length;
    }
}
```



### [57. 和为s的两个数字](https://leetcode.cn/problems/he-wei-sde-liang-ge-shu-zi-lcof/)

> 输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果有多对数字的和等于s，则输出任意一对即可。

示例一：

```java
输入：nums = [2,7,11,15], target = 9
输出：[2,7] 或者 [7,2]
```

示例二：

```java
输入：nums = [10,26,30,31,47,60], target = 40
输出：[10,30] 或者 [30,10]
```

代码：

```java
// 双指针
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int i = 0, j = nums.length - 1;
        while(i < j){
            int sum = nums[i] + nums[j];
            if(sum == target){
                return new int[]{nums[i], nums[j]};
            }else if(sum > target){
                j--;
            }else if(sum < target){
                i++;
            }
        }
        return new int[]{-1,-1};
    }
}
```

### [58 - I. 翻转单词顺序](https://leetcode.cn/problems/fan-zhuan-dan-ci-shun-xu-lcof/)

> 输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。为简单起见，标点符号和普通字母一样处理。例如输入字符串"I am a student. "，则输出"student. a am I"。

示例一：

```java
输入: "the sky is blue"
输出: "blue is sky the"
```

示例二：

```java
输入: "  hello world!  "
输出: "world! hello"
解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
```

示例三：

```java
输入: "a good   example"
输出: "example good a"
解释: 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
```

思路：

> 方法一：双指针
> 倒序遍历字符串s ，记录单词左右索引边界 i , j ；
> 每确定一个单词的边界，则将其添加至单词列表 res ；
> 最终，将单词列表拼接为字符串，并返回即可。
>
> 方法二：分割 + 倒序
> 以空格为分割符完成字符串分割后，若两单词间有 x > 1个空格，则在单词列表 strs中，此两单词间会多出 x - 1 个 “空单词” （即 "" ）。解决方法：倒序遍历单词列表，并将单词逐个添加至 StringBuilder ，遇到空单词时跳过。

代码：

```java
// 双指针：O(N), O(N)
class Solution {
    public String reverseWords(String s) {
        String str = s.trim();
        int j = str.length() - 1, i = j;
        StringBuilder res = new StringBuilder();
        while(i >= 0){
            while(i >= 0 && str.charAt(i) != ' ')   i--;
            res.append(str.substring(i+1, j+1) + " ");
            while(i >= 0 && str.charAt(i) == ' ')   i--;
            j = i;
        }
        return res.toString().trim();
    }
}
// 分割 + 倒序：O(n), O(n)
class Solution {
    public String reverseWords(String s) {
        String[] strs = s.trim().split(" ");
        StringBuilder res = new StringBuilder();
        for(int i = strs.length - 1; i >= 0; i--){
            if(strs[i].equals(""))  continue;
            res.append(strs[i] + " ");
        }
        return res.toString().trim();
    }
}
```



### [58 - II. 左旋转字符串](https://leetcode.cn/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

> 字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

示例一：

```java
输入: s = "abcdefg", k = 2
输出: "cdefgab"
```

示例二：

```java
输入: s = "lrloseumgh", k = 6
输出: "umghlrlose"
```

代码：

```java
// 使用切片函数
class Solution {
    public String reverseLeftWords(String s, int n) {
        return s.substring(n,s.length()) + s.substring(0,n);
    }
}
// 暴力解法，自己做的，果然复杂了，象的太多了
class Solution {
    public String reverseLeftWords(String s, int n) {
        StringBuilder result = new StringBuilder();
        char[] sc = s.toCharArray();
        // 左旋以后的值先加入
        for(int i = n; i < sc.length; i++){
            result.append(sc[i]);
        }
        // 再将左旋的值加入
        for(int i = 0; i < n; i++){
            result.append(sc[i]);
        }
        return result.toString();
    }
}
// 使用StringBuilder，果然别人做的简单
class Solution {
    public String reverseLeftWords(String s, int n) {
        StringBuilder result = new StringBuilder();
        for(int i = n; i < s.length(); i++){
            result.append(s.charAt(i));
        }
        for(int i = 0; i < n; i++){
            result.append(s.charAt(i));
        }
        return result.toString();
    }
}
// 使用取余运算，简化代码
class Solution {
    public String reverseLeftWords(String s, int n) {
        StringBuilder result = new StringBuilder();
        for(int i = n; i < s.length() + n; i++){
            result.append(s.charAt(i%s.length()));
        }
        return result.toString();
    }
}
//只能使用String的方法，进行字符串拼接，直接使用取余的方法简化代码
class Solution {
    public String reverseLeftWords(String s, int n) {
        String res = "";
        for(int i = n; i < n+s.length(); i++){
            res += s.charAt(i % s.length());
        }
        return res;
    }
}
```



## 中等

### [04. 二维数组中的查找](https://leetcode.cn/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

> 在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。
>

示例：

```java
现有矩阵 matrix 如下：
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
给定 target = 5，返回 true。
给定 target = 20，返回 false。
```

思路：

> 方法2: Z字形查找思路：
> 	若 flag > target ，则 target 一定在 flag 所在 行的上方 ，即 flag 所在行可被消去。
> 	若 flag < target ，则 target 一定在 flag 所在 列的右方 ，即 flag 所在列可被消去。
> 从矩阵 matrix 左下角元素（索引设为 (i, j) ）开始遍历，并与目标值对比：
>
>     当 matrix[i][j] > target 时，执行 i-- ，即消去第 i 行元素；
>     当 matrix[i][j] < target 时，执行 j++ ，即消去第 j 列元素；
>     当 matrix[i][j] = target 时，返回 truetrue ，代表找到目标值。
>
> 若行索引或列索引越界，则代表矩阵中无目标值，返回 falsefalse 。

> 方法3：二分查找
> 由于矩阵 matrixmatrix 中每一行的元素都是升序排列的，因此我们可以对每一行都使用一次二分查找，判断 targettarget 是否在该行中，从而判断 targettarget 是否出现。

代码：

```java
//暴力解法：O(N*M)
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        int len = matrix.length;
        if(matrix.length == 0 || matrix[0] == null){
            return false;
        }
        for(int i = 0; i < matrix.length; i++){
            for(int j = 0; j < matrix[0].length; j++){
                if(matrix[i][j] == target){
                    return true;
                }
            }
        }
        return false;
    }
}
//Z字形查找：O(N+M)
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        // 从右上角开始判断
        int i = matrix.length-1;
        int j = 0;
        while(i >= 0 && j < matrix[0].length){
            // 如果当前位置比target大，则向左侧移动
            if(matrix[i][j] > target){
                i--;
            }else if(matrix[i][j] < target){	//如果比target小则向下移动
                j++;
            }else{
                return true;
            }
        }
        return false;
    }
}
//二分查找：O(n*logM)
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        for(int[] row : matrix){
            // 对每一行进行二分查找
            int index = search(row, target);
            if(index >= 0){
                return true;
            }
        }
        return false;
    }
    public int search(int[] arr, int target){
        int low = 0, high = arr.length-1;
        while(low <= high){
            int mid = (high - low) / 2 + low;
            int num = arr[mid];
            if(num == target){
                return mid;
            }else if(num < target){
                low = mid + 1;
            }else{
                high = mid -1;
            }
        }
        return -1;
    }
}
```



### [12. 矩阵中的路径](https://leetcode.cn/problems/ju-zhen-zhong-de-lu-jing-lcof/)

> 给定一个 m x n 二维字符网格 board 和一个字符串单词 word 。如果 word 存在于网格中，返回 true ；否则，返回 false 。
> 单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用

示例一：

```java
输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
输出：true
```

示例二：

```java
输入：board = [["a","b"],["c","d"]], word = "abcd"
输出：false
```

代码：

```java
// DFS + 剪枝：O(MN3^k), O(K)
class Solution {
    public boolean exist(char[][] board, String word) {
        char[] words = word.toCharArray();
        // 循环遍历走每个点，如果找到了真正的起点，就不会再往后遍历
        for(int i = 0; i < board.length; i++){
            for(int j = 0; j < board[0].length; j++){
                if(dfs(board, words, i, j, 0))  return true;	// 如果找到了对应的单词，直接返回
            }
        }
        return false;	//代码到这一步说明没找到，直接返回flase
    }

    public boolean dfs(char[][] board, char[] word, int i, int j, int k){
        if(i < 0 || j < 0 || i >= board.length || j >= board[0].length || board[i][j] != word[k])
            return false;	//递归flase终止条件(剪枝)
        if(k == word.length - 1)    return true;	//递归true终止条件
        // 如果一个dfs到了这一步，说明找到了这个k对应border中的结果
        board[i][j] = '\0';	//已经加入的数据复制空字符，这样可以防止重复调用(只要是非字母的字符都可以)
        // 从在border中找到第k个字符处继续上下左右寻找，进入递归
        boolean res = dfs(board, word, i-1, j, k+1) || dfs(board, word, i+1, j, k+1) || dfs(board, word, i, j-1, k+1) || dfs(board, word, i, j+1, k+1);
        // 如果k不对劲，要回溯，将这一步的k的字符重新交给border，防止后续递归需要
        board[i][j] = word[k];
        return res;
    }
}
```

### [13. 机器人的运动范围](https://leetcode.cn/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)

> 地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

示例一：

```java
输入：m = 2, n = 3, k = 1
输出：3
```

示例二：

```java
输入：m = 3, n = 1, k = 0
输出：1
```

代码：

```java
// dfs
class Solution {
    int res = 0;
    public int movingCount(int m, int n, int k) {
        boolean[][] arr = new boolean[m][n];
        dfs(0, 0, m, n, k, arr);
        return res;
    }
    public void dfs(int i, int j, int m, int n, int k, boolean[][] arr){
        // 计算两个坐标数字的和
        int sum = i % 10 + i / 10 + j % 10 + j / 10;
        // i >= m || j >= n是边界条件的判断，k < sum(i, j)判断当前格子坐标是否满足条件
        // visited[i][j]判断这个格子是否被访问过
        if(i >= m || j >= n || arr[i][j] || sum > k){
            return;
        }
        //标注这个格子被访问过
        arr[i][j] = true;
        res++;
        //把当前格子下边格子的坐标加入到队列中
        dfs(i+1, j, m, n, k, arr);
        //把当前格子右边格子的坐标加入到队列中
        dfs(i, j+1, m, n, k, arr);
    }
}
// bfs
class Solution {
    public int movingCount(int m, int n, int k) {
        //临时变量visited记录格子是否被访问过
        boolean[][] arr = new boolean[m][n];
        int res = 0;
        //创建一个队列，保存的是访问到的格子坐标，是个二维数组
        Queue<int[]> queue = new LinkedList<>();
        //从左上角坐标[0,0]点开始访问，add方法表示把坐标点加入到队列的队尾
        queue.add(new int[]{0, 0});
        while(queue.size() > 0){
            //这里的poll()函数表示的是移除队列头部元素，因为队列是先进先出，从尾部添加，从头部移除
            int[] cur = queue.poll();
            int i = cur[0], j = cur[1];
            //计算两个坐标数字的和
            int sum = i % 10 + i / 10 + j %  10 + j / 10;
            // i >= m || j >= n是边界条件的判断，k < sum(i, j)判断当前格子坐标是否满足条件
            // visited[i][j]判断这个格子是否被访问过
            if(i >= m || j >= n || arr[i][j] || sum > k) continue;
            //标注这个格子被访问过
            arr[i][j] = true;
            res++;
             //把当前格子下边格子的坐标加入到队列中
            queue.offer(new int[]{i+1, j});
            //把当前格子右边格子的坐标加入到队列中
            queue.offer(new int[]{i, j+1});
        }
        return res;
    }
}
```

### [14- I. 剪绳子](https://leetcode.cn/problems/jian-sheng-zi-lcof/)

> 给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m-1] 。请问 k[0]*k[1]*...*k[m-1] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

示例一：

```java
输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1
```

示例二：

```java
输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36
```

思路：

>![image-20230218113722892](/Users/zhoujiajie/Library/Application Support/typora-user-images/image-20230218113722892.png)

代码：

```java
public int cuttingRope(int n) {
  int[] dp = new int[n + 1];
  for (int i = 2; i <= n; i++) {
    int curMax = 0;
    for (int j = 1; j < i; j++) {
      curMax = Math.max(curMax, Math.max(j * (i - j), j * dp[i - j]));
    }
    dp[i] = curMax;
  }
  return dp[n];
}
```

### [16. 数值的整数次方](https://leetcode.cn/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/)

> 实现 [pow(*x*, *n*)](https://www.cplusplus.com/reference/valarray/pow/) ，即计算 x 的 n 次幂函数（即，xn）。不得使用库函数，同时不需要考虑大数问题。

示例一：

```java
输入：x = 2.00000, n = 10
输出：1024.00000
```

示例二：

```java
输入：x = 2.10000, n = 3
输出：9.26100
```

示例三：

```java
输入：x = 2.00000, n = -2
输出：0.25000
解释：2-2 = 1/22 = 1/4 = 0.25
```

思路：

> ![image-20230218152137198](/Users/zhoujiajie/Library/Application Support/typora-user-images/image-20230218152137198.png)

代码：

```java
// O(logN), O(logN)
public double myPow(double x, int n) {
  long N = n;
  return N >= 0 ? quickMul(x, N) : 1.0 / quickMul(x, -N);
}
public double quickMul(double x, long N){
  if(N == 0){
    return 1.0;
  }
  double y = quickMul(x, N /2);
  return N % 2 == 0 ? y * y : y * y * x;
}
```



### [26. 树的子结构](https://leetcode.cn/problems/shu-de-zi-jie-gou-lcof/)

> 输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)
> B是A的子结构， 即 A中有出现和B相同的结构和节点值。

示例一：

```java
输入：A = [1,2,3], B = [3,1]
输出：false
```

示例二：

```java
输入：A = [3,4,5,1,2], B = [4,1]
输出：true
```

代码：

```java
class Solution {
    public boolean isSubStructure(TreeNode A, TreeNode B) {
        // 当树A为空或树B为空时，直接返回false
        if(A == null || B == null){
            return false;
        }
        // 节点A为根节点的子树包含树B, 树B是树A左子树的子结构, 树B是树A右子树的子结构
        return recur(A, B) || isSubStructure(A.left, B) || isSubStructure(A.right, B);
    }

    public boolean recur(TreeNode A, TreeNode B){
        // 当节点 B 为空：说明树 B 已匹配完成
        if(B == null) return true;
        // 当节点 A 为空：说明已经越过树 AA 叶子节点;当节点 AA 和 BB 的值不同：说明匹配失败
        if(A == null || A.val != B.val)  return false;
        // 判断 A 和 B 的左子节点是否相等, 判断 A 和 B 的右子节点是否相等
        return recur(A.left,B.left) && recur(A.right, B.right);
    }
}
```



### [32 - I. 从上到下打印二叉树](https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/)

> 从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

示例一：

```java
输入：[3,9,20,null,null,15,7]
输出：[3,9,20,15,7]
```

代码：

```java
class Solution {
    public int[] levelOrder(TreeNode root) {
        // 当树的根节点为空，则直接返回空列表 []
        if(root == null)    return new int[0];
        // 存放要访问的节点
        Queue<TreeNode> queue = new LinkedList<>();
        ArrayList<Integer> ans = new ArrayList<>();
        // 将根节点加入队列中
        queue.add(root);
        while(!queue.isEmpty()){
            //将队列第一个节点取出来
            TreeNode node = queue.poll();
            // 将节点的值添加到列表中
            ans.add(node.val);
            // 将节点的左孩子加入队列
            if(node.left != null)    queue.add(node.left);
            // 将节点的右孩子加入队列
            if(node.right != null)    queue.add(node.right);
        }
        int[] res = new int[ans.size()];
        for(int i = 0; i < ans.size(); i++){
            res[i] = ans.get(i);
        }
        return res;
    }
}
```

### [32 - III. 从上到下打印二叉树 III](https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)

> 请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。

示例：

```java
输入: [3,9,20,null,null,15,7]
输出：[
  [3],
  [20,9],
  [15,7]
]
```

思路：

>规定二叉树的根节点为第 00 层，如果当前层数是偶数，**从左至右**输出当前层的节点值，否则，**从右至左**输出当前层的节点值.对树进行逐层遍历，用队列维护当前层的所有元素，当队列不为空的时候，求得当前队列的长度size，每次从队列中取出size 个元素进行拓展，然后进行下一次迭代。
>利用「双端队列」的数据结构来维护当前层节点值输出的顺序,双端队列是一个可以在队列任意一端插入元素的队列。在广度优先搜索遍历当前层节点拓展下一层节点的时候我们仍然从左往右按顺序拓展，但是对当前层节点的存储我们维护一个变量 isOrderLeft 记录是从左至右还是从右至左的

代码：

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> ans = new LinkedList<List<Integer>>();
        if (root == null) {
            return ans;
        }
        Queue<TreeNode> nodeQueue = new ArrayDeque<TreeNode>();
        nodeQueue.offer(root);
        // 判断当前层是从左至右还是从右至左的
        boolean isOrderLeft = true;
        while (!nodeQueue.isEmpty()) {
            // 利用「双端队列」的数据结构来维护当前层节点值输出的顺序
            Deque<Integer> levelList = new LinkedList<Integer>();
            int size = nodeQueue.size();
            for (int i = 0; i < size; ++i) {
                TreeNode curNode = nodeQueue.poll();
                if (isOrderLeft) {
                    // 如果从左至右，我们每次将被遍历到的元素插入至双端队列的末尾
                    levelList.offerLast(curNode.val);
                } else {
                    // 如果从右至左，我们每次将被遍历到的元素插入至双端队列的头部
                    levelList.offerFirst(curNode.val);
                }
                if (curNode.left != null) {
                    nodeQueue.offer(curNode.left);
                }
                if (curNode.right != null) {
                    nodeQueue.offer(curNode.right);
                }
            }
            ans.add(new LinkedList<Integer>(levelList));
            // 下一层反方向添加
            isOrderLeft = !isOrderLeft;
        }
        return ans;
    }
}
```



### [35. 复杂链表的复制](https://leetcode.cn/problems/fu-za-lian-biao-de-fu-zhi-lcof/)

> 请实现 copyRandomList 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 next 指针指向下一个节点，还有一个 random 指针指向链表中的任意节点或者 null。

示例一：

```java
输入：head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
输出：[[7,null],[13,0],[11,4],[10,2],[1,0]]
```

示例二：

```java
输入：head = [[1,1],[2,1]]
输出：[[1,1],[2,1]]
```

示例三：

```java
输入：head = [[3,null],[3,0],[3,null]]
输出：[[3,null],[3,0],[3,null]]
```

代码：

```java
// 哈希表
class Solution {
    public Node copyRandomList(Node head) {
        if(head == null) return null;
        Node cur = head;
        Map<Node,Node> map = new HashMap<>();
        // 复制各节点，并建立 “原节点 -> 新节点” 的 Map 映射
        while(cur != null){
            map.put(cur,new Node(cur.val));
            cur = cur.next;
        }
        cur = head;
        // 构建新链表的 next 和 random 指向
        while(cur != null){
            map.get(cur).next = map.get(cur.next);
            map.get(cur).random = map.get(cur.random);
            cur = cur.next;
        }
        return map.get(head);
    }
}
//拼接加拆分
class Solution {
    public Node copyRandomList(Node head) {
        if(head == null)    return null;
        Node cur = head;
        // 复制新结点，构造原结点1->新结点1->原结点2->新结点2
        while(cur != null){
            Node temp = new Node(cur.val);
            temp.next = cur.next;
            cur.next = temp;
            cur = temp.next;
        }
        cur = head;
        // 构建各新节点的 random 指向
        while(cur != null){
            if(cur.random != null){
                cur.next.random = cur.random.next;
            }
            cur = cur.next.next;
        }
        cur = head.next;
        Node pre = head, res = head.next;
        // 拆分两链表
        while(cur.next != null){
            pre.next = pre.next.next;
            cur.next = cur.next.next;
            pre = pre.next;
            cur = cur.next;
        }
        // 当pre到达最后一个原链表最后一个时，此时cur到达新链表最后一位，cur.next==null,不进入下一次循环，pre.next没有赋值
        pre.next = null;
        return res;
    }
}
```

### [38. 字符串的排列](https://leetcode.cn/problems/zi-fu-chuan-de-pai-lie-lcof/)

> 输入一个字符串，打印出该字符串中字符的所有排列。
>
> 你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。

示例一：

```java
输入：s = "abc"
输出：["abc","acb","bac","bca","cab","cba"]
```

代码：

```java
class Solution {
    //为了让递归函数添加结果方便，定义到函数之外，这样无需带到递归函数的参数列表中
    List<String> list = new ArrayList<>();
    //同；但是其赋值依赖c，定义声明分开
    char[] c;
    public String[] permutation(String s) {
        c = s.toCharArray();
        //从第一层开始递归
        dfs(0);
        //将字符串数组ArrayList转化为String类型数组
        return list.toArray(new String[list.size()]);
    }

    private void dfs(int x) {
        //当递归函数到达第三层，就返回，因为此时第二第三个位置已经发生了交换
        if (x == c.length - 1) {
            //将字符数组转换为字符串
            list.add(String.valueOf(c));
            return;
        }
        //为了防止同一层递归出现重复元素
        HashSet<Character> set = new HashSet<>();
        //这里就很巧妙了,第一层可以是a,b,c那么就有三种情况，这里i = x,正巧dfs(0)，正好i = 0开始
        // 当第二层只有两种情况，dfs(1）i = 1开始
        for (int i = x; i < c.length; i++){
            //发生剪枝，当包含这个元素的时候，直接跳过
            if (set.contains(c[i])){
                continue;
            }
            set.add(c[i]);
            //交换元素，这里很是巧妙，当在第二层dfs(1),x = 1,那么i = 1或者 2， 不是交换1和1，要就是交换1和2
            swap(i,x);
            //进入下一层递归
            dfs(x + 1);
            //返回时交换回来，这样保证到达第1层的时候，一直都是abc。这里捋顺一下，开始一直都是abc，那么第一位置总共就3个交换
            //分别是a与a交换，这个就相当于 x = 0, i = 0;
            //     a与b交换            x = 0, i = 1;
            //     a与c交换            x = 0, i = 2;
            //就相当于上图中开始的三条路径
            //第一个元素固定后，每个引出两条路径,
            //     b与b交换            x = 1, i = 1;
            //     b与c交换            x = 1, i = 2;
            //所以，结合上图，在每条路径上标注上i的值，就会非常容易好理解了
            swap(i,x);
        }
    }

    private void swap(int i, int x) {
        char temp = c[i];
        c[i] = c[x];
        c[x] = temp;
    }
}
```

### [44. 数字序列中某一位的数字](https://leetcode.cn/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/)

> 数字以0123456789101112131415…的格式序列化到一个字符序列中。在这个序列中，第5位（从下标0开始计数）是5，第13位是1，第19位是4，等等。
>
> 请写一个函数，求任意第n位对应的数字。

示例一：

```java
输入：n = 3
输出：3
```

示例二：

```java
输入：n = 11
输出：0
```

代码：

```java
// O(logN), O(logN)
public int findNthDigit(int n) {
  int digit = 1;
  long count = 9;
  long start = 1;
  while(n > count){
    n -= count;
    digit += 1;
    start *= 10;
    count = digit * start * 9;
  }
  long num = start + (n-1) / digit;
  return Long.toString(num).charAt((n-1) % digit) - '0';
}
```



### [46. 把数字翻译成字符串](https://leetcode.cn/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/)

> 给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

示例一：

```java
输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
```

代码：

```java
// 动态规划
class Solution {
    public int translateNum(int num) {
        String src = String.valueOf(num);
        int length = src.length();
        if(length < 2){
            return length;
        }
        char[] array = src.toCharArray();
        int[] dp = new int[length];
        dp[0] = 1;
        for(int i = 1; i < length; i++){
            dp[i] = dp[i-1];
            int cur = 10 * (array[i-1] - '0') + array[i] - '0';
            if(cur >= 10 && cur <= 25){
                if(i == 1){
                    dp[i]++;
                }else{
                    dp[i] += dp[i-2];
                }
            }
        }
        return dp[length-1];
    }
}
```

### [47. 礼物的最大价值](https://leetcode.cn/problems/li-wu-de-zui-da-jie-zhi-lcof/)

> 在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？

示例一：

```java
输入: 
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 12
解释: 路径 1→3→5→2→1 可以拿到最多价值的礼物
```

代码：

```java
// 动态规划：O(MN),O(1)
class Solution {
    public int maxValue(int[][] grid) {
        for(int i = 0; i < grid.length; i++){
            for(int j = 0; j < grid[0].length; j++){
                if(i == 0 && j == 0)    continue;
                // 矩阵第一行元素，只可从左边到达
                else if(i == 0) grid[i][j] += grid[i][j-1];
                // 为矩阵第一列元素，只可从上边到达
                else if(j == 0) grid[i][j] += grid[i-1][j];
                // 可从左边或上边到达
                else grid[i][j] += Math.max(grid[i-1][j], grid[i][j-1]);
            }
        }
        return grid[grid.length-1][grid[0].length-1];
    }
}
```

### [48. 最长不含重复字符的子字符串](https://leetcode.cn/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/)

> 请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。

示例一：

```java
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

示例二：

```java
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```

代码：

```java
// 动态规划+哈希表：O(N),O(1)
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> dic = new HashMap<>();
        int res = 0, tmp = 0;
        for(int j = 0; j < s.length(); j++){
            int i = dic.getOrDefault(s.charAt(j), -1);	// 获取索引 i
            dic.put(s.charAt(j), j);	// 更新哈希表
            tmp = tmp < j-i ? tmp+1 : j - i;	// dp[j - 1] -> dp[j]
            res = Math.max(res,tmp);	// max(dp[j - 1], dp[j])
        }
        return res;
    }
}
// 双指针+哈希表：O(N), O(1)
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> dic = new HashMap<>();
        int res = 0, i = -1;
        for(int j = 0; j < s.length(); j++){
            if(dic.containsKey(s.charAt(j))){
                i = Math.max(i, dic.get(s.charAt(j)));	//更新左指针i
            }
            dic.put(s.charAt(j),j);	// 哈希表记录
            res = Math.max(res, j - i);	// 更新结果
        }
        return res;
    }
}
```

### [49. 丑数](https://leetcode.cn/problems/chou-shu-lcof/)

> 我们把只包含质因子 2、3 和 5 的数称作丑数（Ugly Number）。求按从小到大的顺序的第 n 个丑数。

示例一：

```java
输入: n = 10
输出: 12
解释: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 是前 10 个丑数。
```

思路：

> ![image-20230221220044435](/Users/zhoujiajie/Library/Application Support/typora-user-images/image-20230221220044435.png)

代码：

```java
// 动态规划：O(n), O(n)
public int nthUglyNumber(int n) {
  int a = 0, b = 0, c = 0;
  int[] dp = new int[n];
  dp[0] = 1;
  for(int i = 1; i < n; i++){
    int n2 = dp[a] * 2, n3 = dp[b] * 3, n5 = dp[c] * 5;
    dp[i] = Math.min(Math.min(n2, n3), n5);
    if(dp[i] == n2) a++;
    if(dp[i] == n3) b++;
    if(dp[i] == n5) c++; 
  }
  return dp[n-1];
}
```



### [63. 股票的最大利润](https://leetcode.cn/problems/gu-piao-de-zui-da-li-run-lcof/)

> 假设把某股票的价格按照时间先后顺序存储在数组中，请问买卖该股票一次可能获得的最大利润是多少？

示例一：

```java
输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。
```

示例二：

```java
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

代码：

```java
// 动态规划：O(n)
class Solution {
    public int maxProfit(int[] prices) {
        if(prices.length == 0){
            return 0;
        }
        // 把第一天的价格当成是初始最小值,第一天无卖出利润为0
        int min = prices[0], profit = 0;
        // 遍历每天的结果，寻找最大利润
        for(int i = 1; i < prices.length; i++){
            // 更新最低价格（买入价），最低价格应该拿当前的最低价格跟今天的价格对比
            if(prices[i] < min){
                min = prices[i];
            }
            // 更新最大利润，最大利润应该是当前的最大利润与（当前价格 - 最低价格（买入价））对比的最大值
            profit = Math.max(profit, prices[i] - min);
        }
        return profit;
    }
}
```



# 剑指Offer2专项

## 简单

### [001. 整数除法](https://leetcode.cn/problems/xoh6Oh/)

> 给定两个整数 `a` 和 `b` ，求它们的除法的商 `a/b` ，要求不得使用乘号 `'*'`、除号 `'/'` 以及求余符号 `'%'` 

示例一：

```java
输入：a = 15, b = 2
输出：7
解释：15/2 = truncate(7.5) = 7
```

示例二：

```java
输入：a = 7, b = -3
输出：-2
解释：7/-3 = truncate(-2.33333..) = -2
```

示例三：

```java
输入：a = 0, b = 1
输出：0
```

示例四：

```java
输入：a = 1, b = 1
输出：1
```

思路：

> 由于题目要求不能使用乘法、除法以及求余，因此考虑用加法代替乘法。对于 a / b, a、b都是整数，为了缩小讨论范围，假设a、b都是正数，那么商的范围为[0, a]，当a < b或b = 0(无意义)时为0。可以通过不断倍增b并将倍增结果与a比较来找到商，这实际上是一个二分搜索的过程。关键代码如下(a / b = c)。应当注意，b在倍增过程中，若超过最大值的一半，那么b + b会因为溢出得到负数，此时 <= a的判断将导致错误的结果，因此在while条件中要使得b <= Integer.MAX_VALUE / 2。例如a = Integer.MAX_VALUE, b = 1时，b会倍增到1073741824 > Integer.MAX_VALUE / 2 = 1073741823，不满足上述条件跳出循环（短路判断）。由于在有剩余的情况下余下部分的大小需要与b进行比较，因此用d = b来表示除数的倍增变化，用ans来累计商。
>
> 当a、b不同号时，一个自然的想法是按正整数求解，返回结果时再取反即可。按照这个想法，现在来考虑a、b的符号以及edge cases。a、b的范围均为[-2^31, 2^31 - 1]，为方便，定义MIN = -2^31, MAX = 2^31 - 1。可以看到MIN的绝对值比MAX更大，当a = MIN时，对a取反会导致溢出。因此我们反其道而行之，按a、b都为负数处理，这样就可以覆盖所有a、b取值的情形。将前述假设a、b均为正数的代码修正为假设a、b均为负数的版本。另外对于第二个while中的(d + d <= a)，有经验的话不难察觉到d + d的写法可能导致加法溢出，因此改写为d <= a - d。但由于第一个条件已经避免了d + d溢出的情形，因此无需改写。
>
> 题目已经声明b != 0，因此无需考虑这个edge case。唯一需要处理的edge case是a = -2^31, b = -1，此时会溢出，按题目要求应该返回MAX。

代码：

```java
class Solution {
    public int divide(int a, int b) {
        //特判   -2^31/-1=2^31溢出 所以返回2^31-1
        if(a==Integer.MIN_VALUE && b == -1){
            return Integer.MAX_VALUE;
        }
        // 判断商为正还是负
        boolean isPos = (a < 0 && b < 0) || (a > 0 && b > 0) ? true : false;
        // 将整体按照负数进行计算
        if(a > 0) a = -a;
        if(b > 0) b = -b;
        // 商值
        int ans = 0;
        while(a <= b){
            // d为当前除数，c为当前商
            int d = b, c = 1;
            // 第一个条件是防止d+d溢出
            while(d >= Integer.MIN_VALUE >> 1 && d + d >= a){
                d += d; //当前除数倍增 
                c += c; //当前商倍增
            }
            a -= d; //a剩余部分
            ans += c;
        }
        if(isPos){  
            return ans;
        }
        return -ans;
    }
}
```

### [002. 二进制加法](https://leetcode.cn/problems/JFETK5/)

> 给定两个 01 字符串 `a` 和 `b` ，请计算它们的和，并以二进制字符串的形式输出。
>
> 输入为 **非空** 字符串且只包含数字 `1` 和 `0`。

示例一：

```java
输入: a = "11", b = "10"
输出: "101"
```

示例二：

```java
输入: a = "1010", b = "1011"
输出: "10101"
```

代码：

```java
class Solution {
    public String addBinary(String a, String b) {
        StringBuffer ans = new StringBuffer();
        int i = a.length() - 1;
        int j = b.length() - 1;
        int carry = 0;
        while(i >= 0 || j >= 0){
            int sum = carry;	// 把进位计算在本轮内
            if(i >= 0){
                sum += a.charAt(i--) - '0';
            }
            if(j >= 0){
                sum += b.charAt(j--) - '0';
            }
            carry = sum / 2;	//进位
            ans.append(sum % 2);	//当前位
        }
        // 最高位仍有进位时
        if(carry != 0){
            ans.append(carry);
        }
        return ans.reverse().toString();	//翻转
    }
}
```



# Hot 100

## 简单

### [1. 两数之和](https://leetcode.cn/problems/two-sum/)

> 给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。
>
> 你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。
>
> 你可以按任意顺序返回答案。

示例一：

```java
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
```

示例二：

```java
输入：nums = [3,2,4], target = 6
输出：[1,2]
```

代码：

```java
// 暴力循环：O(N^2),O(1)
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int n = nums.length;
        for(int i = 0; i < n; i++){
            for(int j = i+1; j < n; j++){
                if(nums[i] + nums[j] == target){
                    return new int[]{i,j};
                }
            }
        }
        return new int[]{-1,-1};
    }
}
// 哈希表：O(N), O(1)
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> res = new HashMap<>();
        for(int i = 0; i < nums.length; i++){
            if(res.containsKey(target - nums[i])){
                return new int[]{res.get(target - nums[i]), i};
            }
            res.put(nums[i], i);
        }
        return new int[]{-1,-1};
    }
}
```



## 中等

### [2. 两数相加](https://leetcode.cn/problems/add-two-numbers/)

> 给你两个 非空 的链表，表示两个非负的整数。它们每位数字都是按照 逆序 的方式存储的，并且每个节点只能存储 一位 数字。
>
> 请你将两个数相加，并以相同形式返回一个表示和的链表。
>
> 你可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例一：

```java
输入：l1 = [2,4,3], l2 = [5,6,4]
输出：[7,0,8]
解释：342 + 465 = 807.
```

示例二：

```java
输入：l1 = [0], l2 = [0]
输出：[0]
```

代码：

```java
// 模拟
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode prev = new ListNode(0);
        int carry = 0;
        ListNode cur = prev;

        while(l1 != null || l2 != null){
            int x = l1 != null ? l1.val : 0;
            int y = l2 != null ? l2.val : 0;
            int sum = x + y + carry;
            carry = sum / 10;
            sum = sum % 10;
            cur.next = new ListNode(sum);
            cur = cur.next;
            if(l1 != null){
                l1 = l1.next;
            }
            if(l2 != null){
                l2 = l2.next;
            }
        }
        if(carry == 1){
            cur.next = new ListNode(1);
        }
        return prev.next;
    }
}
```

### [3. 无重复字符的最长子串](https://leetcode.cn/problems/longest-substring-without-repeating-characters/)

> 给定一个字符串 `s` ，请你找出其中不含有重复字符的 **最长子串** 的长度。

示例一：

```java
输入: s = "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

示例二：

```java
输入: s = "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

代码：

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int right = 0, ans = 0;
        // 哈希集合，记录每个字符是否出现过
        Set<Character> set = new HashSet<>();
        for(int i = 0; i < s.length(); i++){
            // 左指针向右移动一格，移除一个字符
            if(i != 0)  set.remove(s.charAt(i-1));
            while(right < s.length() && !set.contains(s.charAt(right))){
                // 不断地移动右指针
                set.add(s.charAt(right));
                right++;
            }
            ans = Math.max(ans, right-i);
        }
        return ans;
    }
}
```



# CodeTop

## [3. 无重复字符的最长子串](https://leetcode.cn/problems/longest-substring-without-repeating-characters/)

> 给定一个字符串 `s` ，请你找出其中不含有重复字符的 **最长子串** 的长度。

代码：

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int right = 0, ans = 0;
        // 哈希集合，记录每个字符是否出现过
        Set<Character> set = new HashSet<>();
        for(int i = 0; i < s.length(); i++){
            // 左指针向右移动一格，移除一个字符
            if(i != 0)  set.remove(s.charAt(i-1));
            while(right < s.length() && !set.contains(s.charAt(right))){
                // 不断地移动右指针
                set.add(s.charAt(right));
                right++;
            }
            ans = Math.max(ans, right-i);
        }
        return ans;
    }
}
```

## [206. 反转链表](https://leetcode.cn/problems/reverse-linked-list/)

> 给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。

代码：

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
// 迭代
class Solution {
    public ListNode reverseList(ListNode head) {
       if(head == null || head.next == null){
           return head;
       }
       ListNode newHead = reverseList(head.next);
       head.next.next = head;
       head.next = null;
       return newHead;
    }
}
class Solution {
    public ListNode reverseList(ListNode head) {
       ListNode pre = null;
       ListNode cur = head;
       while(cur != null){
           ListNode next = cur.next;
           cur.next = pre;
           pre = cur;
           cur = next;
       }
       return pre;
    }
}
```

## 146. LRU缓存

> 请你设计并实现一个满足  LRU (最近最少使用) 缓存 约束的数据结构。
> 实现 LRUCache 类：
> LRUCache(int capacity) 以 正整数 作为容量 capacity 初始化 LRU 缓存
> int get(int key) 如果关键字 key 存在于缓存中，则返回关键字的值，否则返回 -1 。
> void put(int key, int value) 如果关键字 key 已经存在，则变更其数据值 value ；如果不存在，则向缓存中插入该组 key-value 。如果插入操作导致关键字数量超过 capacity ，则应该 逐出 最久未使用的关键字。
> 函数 get 和 put 必须以 O(1) 的平均时间复杂度运行。

思路：

> ![image-20230306144705352](/Users/zhoujiajie/Library/Application Support/typora-user-images/image-20230306144705352.png)

代码：

```java
class LRUCache {

    class DLinkedNode{
        int key;
        int value;
        DLinkedNode pre;
        DLinkedNode next;
        public DLinkedNode(){}
        public DLinkedNode(int _key, int _value){
            key = _key;
            value = _value;

        }
    }

    private Map<Integer, DLinkedNode> cache = new HashMap<>();
    private int size;
    private int capacity;
    public DLinkedNode head, tail;

    public LRUCache(int capacity) {
        this.size = 0;
        this.capacity = capacity;
        head = new DLinkedNode();
        tail = new DLinkedNode();
        head.next = tail;
        tail.pre = head;
    }
    
    public int get(int key) {
        DLinkedNode node = cache.get(key);
        if(node == null){
            return -1;
        }
        moveToHead(node);
        return node.value;
    }
    
    public void put(int key, int value) {
        DLinkedNode node = cache.get(key);
        if(node == null){
            DLinkedNode newNode = new DLinkedNode(key,value);
            cache.put(key, newNode);
            addToHead(newNode);
            ++size;
            if(size > capacity){
                DLinkedNode tail = removeTail();
                cache.remove(tail.key);
                --size;
            }
        }else{
            node.value = value;
            moveToHead(node);
        }
    }

    public void addToHead(DLinkedNode node){
        node.pre = head;
        node.next = head.next;
        head.next.pre = node;
        head.next = node;
    }

    public void removeNode(DLinkedNode node){
        node.pre.next = node.next;
        node.next.pre = node.pre;
    }

    public void moveToHead(DLinkedNode node){
        removeNode(node);
        addToHead(node);
    }

    public DLinkedNode removeTail(){
        DLinkedNode res = tail.pre;
        removeNode(res);
        return res;
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

## [215. 数组中的第K个最大元素](https://leetcode.cn/problems/kth-largest-element-in-an-array/)

> 给定整数数组 nums 和整数 k，请返回数组中第 k 个最大的元素。
>
> 请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。
>
> 你必须设计并实现时间复杂度为 O(n) 的算法解决此问题。

代码：

```java
// 快速排序，随机快排O(n), O(1)
import java.util.Random;
// O(n), O(1)
class Solution {
    private final static Random random = new Random(System.currentTimeMillis());
    public int findKthLargest(int[] nums, int k) {
        int len = nums.length;
        int target = len - k;
        int left = 0;
        int right = nums.length - 1;
        while(true){
            int pivotIndex = partition(nums, left, right);
            if(pivotIndex == target){
                return nums[pivotIndex];
            } else if(pivotIndex < target){
                left = pivotIndex + 1;
            }else{
                right = pivotIndex - 1;
            }
        }
    }

    private int partition(int[] nums, int left, int right){
        int randomIndex = left + random.nextInt(right - left + 1);
        swap(nums, left, randomIndex);
        int pivot = nums[left];
        int le = left + 1;
        int ge = right;

        while(true){
            while(le <= ge && nums[le] < pivot){
                le++;
            }
            while(le <= ge && nums[ge] > pivot){
                ge--;
            }
            if(le >= ge){
                break;
            }
            swap(nums, le, ge);
            le++;
            ge--;

        }
        swap(nums, ge, left);
        return ge;
    }

    private void swap(int[] nums, int index1, int index2){
        int tmp = nums[index1];
        nums[index1] = nums[index2];
        nums[index2] = tmp;
    }
}
```

## [25. K 个一组翻转链表](https://leetcode.cn/problems/reverse-nodes-in-k-group/)

> 给你链表的头节点 head ，每 k 个节点一组进行翻转，请你返回修改后的链表。
>
> k 是一个正整数，它的值小于或等于链表的长度。如果节点总数不是 k 的整数倍，那么请将最后剩余的节点保持原有顺序。
>
> 你不能只是单纯的改变节点内部的值，而是需要实际进行节点交换。

代码：

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode hair = new ListNode(0);
        hair.next = head;
        ListNode pre = hair;
        ListNode end = hair;

        while(end.next != null){
            for(int i = 0; i < k && end != null; i++){
                end = end.next;
            }
            if(end == null) break;
            ListNode start = pre.next;
            ListNode next = end.next;
            end.next = null;
            pre.next = reverse(start);
            start.next = next;
            pre = start;
            end = pre;
        }
        return hair.next;
    }

    public ListNode reverse(ListNode head){
        ListNode pre = null;
        ListNode cur = head;
        while(cur != null){
            ListNode next = cur.next;
            cur.next = pre;
            pre = cur;
            cur = next;
        }
        return pre;
    }
  /*
  // 迭代方式进行反转链表
 		public ListNode reverse(ListNode head){
        if(head == null || head.next == null){
            return head;
        }
        ListNode newHead = reverse(head.next);
        head.next.next = head;
        head.next = null;
        return newHead;
    }
   */
}
```

## [15. 三数之和](https://leetcode.cn/problems/3sum/)

> 给你一个整数数组 nums ，判断是否存在三元组 [nums[i], nums[j], nums[k]] 满足 i != j、i != k 且 j != k ，同时还满足 nums[i] + nums[j] + nums[k] == 0 。请
>
> 你返回所有和为 0 且不重复的三元组。
>

代码：

```java
public List<List<Integer>> threeSum(int[] nums) {
  int n = nums.length;
  Arrays.sort(nums);
  List<List<Integer>> ans = new ArrayList<>();
  //枚举a
  for(int first = 0; first < n; first++){
    //要求与上次枚举的元素不同
    if(first > 0 && nums[first] == nums[first-1]){
      continue;
    }
    //指针c最初指向数组最右端
    int third = n - 1;
    int target = -nums[first];
    //枚举b
    for(int second = first + 1; second < n; second++){
      //要求与上次枚举的元素不同
      if(second > first + 1 && nums[second] == nums[second - 1]){
        continue;
      }
      //保证指针b在指针c的左侧
      while(second < third && nums[second] + nums[third] > target){
        third--;
      }
      if(second == third){
        break;
      }
      if(nums[second] + nums[third] == target){
        List<Integer> list = new ArrayList<>();
        list.add(nums[first]);
        list.add(nums[second]);
        list.add(nums[third]);
        ans.add(list);
      }
    }
  }
  return ans;
}
```

## [53. 最大子数组和](https://leetcode.cn/problems/maximum-subarray/)

> 给你一个整数数组 `nums` ，请你找出一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。
>
> **子数组** 是数组中的一个连续部分。

代码：

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int pre = 0, maxAns = nums[0];
        for(int num : nums){
            pre = Math.max(num, pre + num);
            maxAns = Math.max(pre, maxAns);
        }
        return maxAns;
    }
}
```

## [912. 排序数组](https://leetcode.cn/problems/sort-an-array/)

> 给你一个整数数组 `nums`，请你将该数组升序排列。

代码：

```java
// 随机快排：时间复杂度O(nlogn)
class Solution {
    private final static Random random = new Random(System.currentTimeMillis());

    public int[] sortArray(int[] nums) {
        quickSort(nums, 0, nums.length - 1);
        return nums;
    }

    public void quickSort(int[] nums, int left, int right){
        if(left < right){
            int pos = partition(nums, left, right);
            quickSort(nums, left, pos-1);
            quickSort(nums, pos+1, right);
        }
    }

    public int partition(int[] nums, int left, int right){
        int randomIndex = left + random.nextInt(right - left + 1);
        swap(nums, left, randomIndex);
        int pivot = nums[left];
        int le = left + 1;
        int ge = right;
        while(true){
            while(le <= ge && nums[le] < pivot){
                le++;
            }
            while(le <= ge && nums[ge] > pivot){
                ge--;
            }
            if(le >= ge){
                break;
            }
            swap(nums, le, ge);
            le++;
            ge--;
        }
        swap(nums, ge, left);
        return ge;
    }

    public void swap(int[] nums, int i, int j){
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
// 堆排序，建立大根堆：O(nlogn), O(1)
class Solution {
    public int[] sortArray(int[] nums) {
        heapSort(nums);
        return nums;
    }

    public void heapSort(int[] nums) {
        int len = nums.length - 1;
        buildMaxHeap(nums, len);
        for (int i = len; i >= 1; --i) {
            swap(nums, i, 0);
            len -= 1;
            maxHeapify(nums, 0, len);
        }
    }

    public void buildMaxHeap(int[] nums, int len) {
        for (int i = len / 2; i >= 0; --i) {
            maxHeapify(nums, i, len);
        }
    }

    public void maxHeapify(int[] nums, int i, int len) {
        for (; (i << 1) + 1 <= len;) {
            int lson = (i << 1) + 1;
            int rson = (i << 1) + 2;
            int large;
            if (lson <= len && nums[lson] > nums[i]) {
                large = lson;
            } else {
                large = i;
            }
            if (rson <= len && nums[rson] > nums[large]) {
                large = rson;
            }
            if (large != i) {
                swap(nums, i, large);
                i = large;
            } else {
                break;
            }
        }
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
// 归并排序：O(nlogn), O(n)
class Solution {
    int[] tmp;

    public int[] sortArray(int[] nums) {
        tmp = new int[nums.length];
        mergeSort(nums, 0, nums.length - 1);
        return nums;
    }

    public void mergeSort(int[] nums, int l, int r) {
        if (l >= r) {
            return;
        }
        int mid = (l + r) >> 1;
        mergeSort(nums, l, mid);
        mergeSort(nums, mid + 1, r);
        int i = l, j = mid + 1;
        int cnt = 0;
        while (i <= mid && j <= r) {
            if (nums[i] <= nums[j]) {
                tmp[cnt++] = nums[i++];
            } else {
                tmp[cnt++] = nums[j++];
            }
        }
        while (i <= mid) {
            tmp[cnt++] = nums[i++];
        }
        while (j <= r) {
            tmp[cnt++] = nums[j++];
        }
        for (int k = 0; k < r - l + 1; ++k) {
            nums[k + l] = tmp[k];
        }
    }
}
```

