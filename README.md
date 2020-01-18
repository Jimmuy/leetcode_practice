# leetcode_practice
A project for arithmetic study , daily update        

[1.给定一个大小为 n 的数组，找到其中的多数元素。多数元素是指在数组中出现次数大于 ⌊ n/2 ⌋ 的元素。](#1.给定一个大小为n的数组。找到其中的多数元素。多数元素是指在数组中出现次数大于⌊n/2⌋的元素)

[2.给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。](#2.给定一个数组nums，编写一个函数将所有0移动到数组的末尾，同时保持非零元素的相对顺序。)

[3.448. 找到所有数组中消失的数字](#3.给定一个范围在1≤a[i]≤n(n=数组大小)的整型数组，数组中的元素一些出现了两次，另一些只出现一次。)

[3.121.买卖股票的最佳时机](#4.121.买卖股票的最佳时机)

[4.53. 最大子序和](#4.53.最大子序和)


[5.1. 两数之和](#5.1.两数之和)


[6.581. 最短无序连续子数组](#6.581.最短无序连续子数组)

[7.78.子集](#7.78.子集)

[8.39.组合总和I](#8.39.组合总和)

[9.40.组合总和II](#9.40.组合总和II)

[10.90.子集II](#10.90.子集II)

[11.46.全排列](#10.46.全排列)

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

# 53.最大子序和

给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

示例:

输入: [-2,1,-3,4,-1,2,1,-5,4],
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
进阶:

如果你已经实现复杂度为 O(n) 的解法，尝试使用更为精妙的分治法求解。

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
题解：
```
public int maxSubArray(int[] nums) {
        // 思路：贪心算法 设置最大和，和当前最大和，遍历
        // 最大子序和[-2,1,-3,4,-1,2,1,-5,4]
        int maxSum = nums[0];
        int currentSum = nums[0];
        for (int i = 1; i < nums.length; ++i) {
            //若当前位置大于前面的和，指针就会移动到当前位置
            currentSum = Math.max(currentSum + nums[i], nums[i]);
            maxSum = Math.max(maxSum, currentSum);
        }
        return maxSum;
    }
```
# 5.1.两数之和

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

示例:

给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]

题解：
```
    public int[] twoSum(int[] nums, int target) {
          //使用hash表存储相应的数据，在一次遍历中根据遍历到的元素去哈希表中去查询是否有target-num[i]对应的值，如果有就是所需要的答案
        int length = nums.length;
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < length; i++) {
            if (map.containsKey(target - nums[i])) {
                return new int[]{map.get(target - nums[i]),i};
            } else {
                map.put(nums[i],i);
            }
        }
        return null;  
    }
```
# 6.581.最短无序连续子数组

给定一个整数数组，你需要寻找一个连续的子数组，如果对这个子数组进行升序排序，那么整个数组都会变为升序排序。

你找到的子数组应是最短的，请输出它的长度。

示例 1:

输入: [2, 6, 4, 8, 10, 9, 15]
输出: 5
解释: 你只需要对 [6, 4, 8, 10, 9] 进行升序排序，那么整个表都会变为升序排序。
说明 :

输入的数组长度范围在 [1, 10,000]。
输入的数组可能包含重复元素 ，所以升序的意思是<=。


# 7.78.子集

给定一组不含重复元素的整数数组 nums，返回该数组所有可能的子集（幂集）。

```
        public static int findUnsortedSubarray(int[] nums) {
        //本题目查找的就是左边界和右边界的问题，
        // 最开始的想法是使用两个循环一个正着找左边界，
        // 一个倒着找右边界，后来发现可以合并为一个循环
        int length = nums.length;
        int max = nums[0];
        int min = nums[length - 1];
        int right = -1;
        int left = 0;
        for (int i = 0; i < length; i++) {
            //如果右边有比max还大的值，则赋值给max,如果遇到了小于max的值说明顺序要调整
            if (nums[i] >= max) {
                max = nums[i];
            } else {
                right = i;
            }
            //同理找最小值和左边界
            if (nums[length - i - 1] <= min) {
                min = nums[length - i - 1];
            } else {
                left = length - i - 1;
            }
        }
        return right - left + 1;
    }
```

```
 public List<List<Integer>> subsets(int[] nums) {
        //思路 使用while循环控制当前添加进数组的长度 内循环for用来向数组中添加值
        List<List<Integer>> result = new ArrayList<>();
        result.add(new ArrayList<Integer>());
        for (Integer n : nums) {
            //内循环的循环次数，因为要从result取值，所以最大角标就是result的当前size
            int size = result.size();
            for (int i = 0; i < size; i++) {
                //每次从result数组中添加轮训的值
                List<Integer> list = new ArrayList<>(result.get(i));
                list.add(n);
                result.add(list);
            }
        }
        return result;
    }

    public List<List<Integer>> subsets2(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        //二进制做法
        //一共1<<nums.length个数
        for (int i = 0; i <( 1 << nums.length); i++) {
            List<Integer> list = new ArrayList<>();
            for (int j = 0; j < nums.length; j++) {
                //每次循环先找(i >> j) & 1为1的值若为1则添加进来
                if (((i >> j) & 1) == 1) list.add(j);
            }
            result.add(list);
        }
        return result;
    }
```
# 8.39.组合总和 

给定一个无重复元素的数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

candidates 中的数字可以无限制重复被选取。

说明：

所有数字（包括 target）都是正整数。
解集不能包含重复的组合。 
示例 1:

输入: candidates = [2,3,6,7], target = 7,
所求解集为:
[
  [7],
  [2,2,3]
]
示例 2:

输入: candidates = [2,3,5], target = 8,
所求解集为:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]


题解：
（39和40）题为类似问题，采用回溯算法的方式进行求解，解答的过程中采用画图的方式找到解答题目的思路，两道题目中唯一的不同点是一个可以使用重复的元素而一个不可以使用，这就使得这道题目的解题思路一致。

```
 List<List<Integer>> result;

    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        result = new ArrayList<>();
        //边界条件判断
        if (candidates == null || candidates.length <= 0) {
            return result;
        }
        Arrays.sort(candidates);
        List<Integer> list = new ArrayList<>();
        helper(candidates, list, 0, target);
        return result;
    }

    public void helper(int[] cadidaes, List<Integer> list, int index, int target) {
        if (target == 0) {
            result.add(new ArrayList<>(list));
            return;
        }
        for (int i = index; i < cadidaes.length && target >= cadidaes[i]; i++) {
            list.add(cadidaes[i]);
            //遍历过程中采用重复的元素
            helper(cadidaes, list, i, target - cadidaes[i]);
            list.remove(list.size()-1);
        }

    }
```

# 9.40.组合总和II
给定一个数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

candidates 中的每个数字在每个组合中只能使用一次。

说明：

所有数字（包括目标数）都是正整数。
解集不能包含重复的组合。 
示例 1:

输入: candidates = [10,1,2,7,6,1,5], target = 8,
所求解集为:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
示例 2:

输入: candidates = [2,5,2,1,2], target = 5,
所求解集为:
[
  [1,2,2],
  [5]
]
```
List<List<Integer>> result;
       public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        result = new ArrayList<>();
        if (candidates == null || candidates.length <= 0) {
            return result;
        }
        Arrays.sort(candidates);
        helper2(candidates, new ArrayList<Integer>(), 0, target);
        return result;
    }

    public void helper2(int[] cadidaes, List<Integer> list, int index, int target) {
        if (target == 0) {
            if (!result.contains(list)) {
                result.add(new ArrayList<>(list));
            }
            return;
        }
        for (int i = index; i < cadidaes.length && target >= cadidaes[i]; i++) {
            list.add(cadidaes[i]);
            //遍历过程中不采用重复的元素，将index移动到下个元素
            helper2(cadidaes, list, ++index, target - cadidaes[i]);
            list.remove(list.size() - 1);
        }

    }
```
# 10.90.子集II
给定一个可能包含重复元素的整数数组 nums，返回该数组所有可能的子集（幂集）。

说明：解集不能包含重复的子集。

示例:

输入: [1,2,2]
输出:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```
public List<List<Integer>> subsetsWithDup(int[] num) {
    List<List<Integer>> result = new ArrayList<List<Integer>>();
    List<Integer> empty = new ArrayList<Integer>();
    result.add(empty);
    Arrays.sort(num);

    for (int i = 0; i < num.length; i++) {
        int dupCount = 0;
        //判断当前是否是重复数字，并且记录重复的次数
        while( ((i+1) < num.length) && num[i+1] == num[i]) {
            dupCount++;
            i++;
        }
        int prevNum = result.size();
        //遍历之前几个结果的每个解
        for (int j = 0; j < prevNum; j++) {
            List<Integer> element = new ArrayList<Integer>(result.get(j));
            //每次在上次的结果中多加 1 个重复数字
            for (int t = 0; t <= dupCount; t++) {
                element.add(num[i]); //加入当前重复的数字
                result.add(new ArrayList<Integer>(element));
            }
        }
    }
    return result;
}

```

# 46.全排列


给定一个没有重复数字的序列，返回其所有可能的全排列。

示例:

输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]

```
    public  void backtrack(int[] nums, int length, List<Integer> list, List<List<Integer>> output, int depth, boolean[] used) {
        if (depth == length) {
            //当深度和长度一样的时候则，就是答案
            output.add(new ArrayList<>(list));
            return;
        }
        for (int i = 0; i < length; i++) {
            if (!used[i]) {
                //如果当前没有用过，则进入下一层
                list.add(nums[i]);
                used[i] = true;
                backtrack(nums, length, list, output, depth + 1, used);
                //回溯
                used[i] = false;
                list.remove(depth);
            }
        }
    }

    public  List<List<Integer>> permute(int[] nums) {
        int length = nums.length;
        List<List<Integer>> output = new LinkedList<>();
        ArrayList<Integer> nums_lst = new ArrayList<>();
        boolean[] used = new boolean[length];
        backtrack(nums, length, nums_lst, output, 0, used);
        return output;
    }
```