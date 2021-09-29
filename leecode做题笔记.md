# 数组

## [1. 两数之和](https://leetcode-cn.com/problems/two-sum/)

> > 给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出和为目标值 target 的那两个整数，并返回它们的数组下标。
> >
> > 你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。
> >
> > 你可以按任意顺序返回答案。

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