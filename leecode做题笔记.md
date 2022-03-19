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

> 二分查找的做法是，定义查找的范围 [left,right][\textit{left}, \textit{right}][left,right]，初始查找范围是整个数组。每次取查找范围的中点 mid，比较 nums[mid]和 target 的大小，如果相等则 mid即为要寻找的下标，如果不相等则根据 nums[mid]和 target的大小关系将查找范围缩小一半。
>
> 由于每次查找都会将查找范围缩小一半，因此二分查找的时间复杂度是 O(log⁡n)O(\log n)O(logn)，其中 nnn 是数组的长度。
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



## 中等题



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



# 交互

## 简单

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

