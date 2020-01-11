# leetcode_practice
A project for arithmetic study , daily update        

[1.给定一个大小为 n 的数组，找到其中的多数元素。多数元素是指在数组中出现次数大于 ⌊ n/2 ⌋ 的元素。](#1.给定一个大小为n的数组。找到其中的多数元素。多数元素是指在数组中出现次数大于⌊n/2⌋的元素)

[2.给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。](#2.给定一个数组nums，编写一个函数将所有0移动到数组的末尾，同时保持非零元素的相对顺序。)

[3.448. 找到所有数组中消失的数字](#3.给定一个范围在1≤a[i]≤n(n=数组大小)的整型数组，数组中的元素一些出现了两次，另一些只出现一次。)

[3.121.买卖股票的最佳时机](#4.121.买卖股票的最佳时机)

# 1.给定一个大小为 n 的数组，找到其中的多数元素。多数元素是指在数组中出现次数大于 ⌊ n/2 ⌋ 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

示例 1:
输入: [3,2,3]
输出: 3

示例 2:
输入: [2,2,1,1,1,2,2]
输出: 2

解题：

```
    public int majorityElement(int[] nums) {
        //投票算法
        int count = 1;
        //将起始值作为计数开始的值
        int temp = nums[0];

        for (int i = 1; i < nums.length; i++) {
            //若遇到一样的+1遇到不一样的-1
            if (temp == nums[i]) {
                count++;
            } else {
                count--;
            }
            if (count == 0) {
                //当计数器重新为0的时候说明前面的数全都抵消，假设下一个数为众数。题目假设必有众数，也就是该数出现的次数比其他数加起来出现的次数都多
                temp = nums[i + 1];
            }
        }
        return temp;
    }
```
优化后：
```
    public int majorityElement(int[] nums) {
        //投票算法
        int count = 0;
        //将起始值作为计数开始的值
        Integer temp = null;
        for (Integer num : nums) {
            //若计数器为0，则将循环中的元素赋值给temp
            if (count == 0) temp = num;
            //计算count值，进行下一次轮询
            count += temp.equals(num) ? 1 : -1;
        }
        return temp;
    }
```
# 2.给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。

示例:

输入: [0,1,0,3,12]
输出: [1,3,12,0,0]
说明:

必须在原数组上操作，不能拷贝额外的数组。
尽量减少操作次数。

题解：
```
    public void moveZeroes(int[] nums) {
        //思路 1.使用index记录下当前不为0的数的位置
        int index = 0;
        for (Integer num : nums) {
            if (num != 0) {
                //将每个不等于0的数字按照顺序往数组中排列，并增加index值
                nums[index++] = num;
            }
        }
        //最后将index后面的值赋值为0
        while (nums.length - index > 0) {
            nums[index++] = 0;
        }
    }
```

# 3.给定一个范围在1≤a[i]≤n(n=数组大小)的整型数组，数组中的元素一些出现了两次，另一些只出现一次。

找到所有在 [1, n] 范围之间没有出现在数组中的数字。

您能在不使用额外空间且时间复杂度为O(n)的情况下完成这个任务吗? 你可以假定返回的数组不算在额外空间内。

示例:

输入:
[4,3,2,7,8,2,3,1]

输出:
[5,6]


题解：
```
     public List<Integer> findDisappearedNumbers(int[] nums) {
        List<Integer> result = new ArrayList<>();
        //思路：因为要求原地且要求0（N），所以暴力解法不符合要求
        //遍历所有元素，以当前遍历到的值为数组的下标，将对应下标的值置成负数，遍历到的值使用绝对值去计算角标
        for (Integer num: nums) {
        //遍历所有元素，然后将对应下标的值置成负数
            nums[Math.abs(num)-1] = -Math.abs(nums[Math.abs(num)-1]);
        }
        for (int i = 1; i <=nums.length; i++) {
        //遍历所有值，发现值为正数值位置的角标即为数组中缺省的数字
            if (nums[i-1]>0){
                result.add(i);
            }
        }
        return result;
    }
```
# 4.121.买卖股票的最佳时机
给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

如果你最多只允许完成一笔交易（即买入和卖出一支股票），设计一个算法来计算你所能获取的最大利润。

注意你不能在买入股票前卖出股票。

示例 1:

输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。
示例 2:

输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。


题解：
```
//寻找谷底谷峰[7,1,5,3,6,4],记录最大收益和最小价格，然后依次与当前价格和收益比较
public int maxProfit(int[] prices) {
        if(prices.length<=0){
                return 0;
            }
        //定义最大收益和最小价格
        int max = 0;
        int minPrice = prices[0];
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] < minPrice) {
                //如果当天的价格比最小价格还要小，赋值最小价格
                minPrice = prices[i];
            } else if (max < prices[i] - minPrice) {
                max = prices[i] - minPrice;
            }
        }
        return max;
    }
```
