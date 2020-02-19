# leetcode practice
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

[12.47.全排列II](#12.47.全排列II)

[13.617合并二叉树](#13.617合并二叉树)

[14.1281.整数的各位积和之差](#14.1281.整数的各位积和之差)

[15.1295.统计位数为偶数的数字](#15.1295.统计位数为偶数的数字)

[16.1323.6和9组成的最大数字](#16.1323.6和9组成的最大数字)

[17.1266.访问所有点的最小时间](#17.1266.访问所有点的最小时间)

[18.1290.二进制链表转整数](#18.1290.二进制链表转整数) 

[19.1221.分割平衡字符串](#19.1221.分割平衡字符串)

[20.226. 翻转二叉树](#20.226.翻转二叉树)

[21.938.二叉搜索树的范围和](#21.938.二叉搜索树的范围和)

[22.1304.和为零的N个唯一整数](#22.1304.和为零的N个唯一整数)

[23.728.自除数](#23.728.自除数)

[24.804.唯一摩尔斯密码词](#24.804.唯一摩尔斯密码词)

[25.1299.将每个元素替换为右侧最大元素](#25.1299.将每个元素替换为右侧最大元素)

[26.476.数字的补数](#26.476.数字的补数)

[27.942.增减字符串匹配](#27.942.增减字符串匹配)

[28.206.反转链表](#28.206.反转链表)

[29.146.LRU缓存机制](#29.146.LRU缓存机制)

[30.349.两个数组的交集](#30.349.两个数组的交集)

[31.961.重复N次的元素](#31.961.重复N次的元素)

[32.977.有序数组的平方](#32.977.有序数组的平方)

[33.509.斐波那契数](#33.509.斐波那契数)

[34.160.相交链表](#34.160.相交链表)

[35.21.合并两个有序链表](#35.21.合并两个有序链表)

[36.22.链表中倒数第k个节点](#36.22.链表中倒数第k个节点)

[37.70.爬楼梯](#37.70.爬楼梯)

[38.面试题01.01.判定字符是否唯一](#38.面试题01.01.判定字符是否唯一)

[39.面试题01.02.判定是否互为字符重排、](#39.面试题01.02.判定是否互为字符重排)


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

# 11.46.全排列


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
# 12.47.全排列II

给定一个可包含重复数字的序列，返回所有不重复的全排列。

示例:

输入: [1,1,2]
输出:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]

```
  public static List<List<Integer>> permuteUnique(int[] nums) {
        //先排列出所有的可能,和上一题相比较只是多了一步去重工作
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> list = new ArrayList<>();
        //是否使用过当前节点深度
        int length = nums.length;
        boolean[] isUsed = new boolean[length];
        helper(nums, length, result, list, isUsed, 0);
        return result;
    }

    private static void helper(int[] nums, int length, List<List<Integer>> result, List<Integer> list, boolean[] isUsed, int depth) {
        ArrayList<Integer> element = new ArrayList<>(list);
        //去重元素
        if (length == depth && !result.contains(element)) {
            result.add(element);
            return;
        }

        for (int i = 0; i < length; i++) {
            if (!isUsed[i]) {
                list.add(nums[i]);
                isUsed[i] = true;
                helper(nums, length, result, list, isUsed, depth + 1);
                isUsed[i] = false;
                list.remove(depth);
            }
        }
    }
```
# 13.617合并二叉树
给定两个二叉树，想象当你将它们中的一个覆盖到另一个上时，两个二叉树的一些节点便会重叠。

你需要将他们合并为一个新的二叉树。合并的规则是如果两个节点重叠，那么将他们的值相加作为节点合并后的新值，否则不为 NULL 的节点将直接作为新二叉树的节点。

示例 1:

输入: 
	Tree 1                     Tree 2                  
          1                         2                             
         / \                       / \                            
        3   2                     1   3                        
       /                           \   \                      
      5                             4   7                  
输出: 
合并后的树:
	     3
	    / \
	   4   5
	  / \   \ 
	 5   4   7
注意: 合并必须从两个树的根节点开始。
```
  public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        if (t1 == null)
            return t2;
        if (t2 == null)
            return t1;
        t1.val += t2.val;
        t1.left = mergeTrees(t1.left, t2.left);
        t1.right = mergeTrees(t1.right, t2.right);
        return t1;
    }
```
# 14.1281.整数的各位积和之差

给你一个整数 n，请你帮忙计算并返回该整数「各位数字之积」与「各位数字之和」的差。

 

示例 1：

输入：n = 234
输出：15 
解释：
各位数之积 = 2 * 3 * 4 = 24 
各位数之和 = 2 + 3 + 4 = 9 
结果 = 24 - 9 = 15
示例 2：

输入：n = 4421
输出：21
解释： 
各位数之积 = 4 * 4 * 2 * 1 = 32 
各位数之和 = 4 + 4 + 2 + 1 = 11 
结果 = 32 - 11 = 21
 

提示：

1 <= n <= 10^5

```
    //这种题目才配叫做简单
    public int subtractProductAndSum(int n) {
        int product = 1;
        int plus = 0;
        while (n/10 > 0) {
            int num = n % 10;
            product *= num;
            plus += num;
            n = n / 10;
            if (n < 10) {
                int i = product * n - plus - n;
                return i;
            }

        }
        return 0;   
    }
```

# 15.1295.统计位数为偶数的数字

给你一个整数数组 nums，请你返回其中位数为 偶数 的数字的个数。

 

示例 1：

输入：nums = [12,345,2,6,7896]
输出：2
解释：
12 是 2 位数字（位数为偶数） 
345 是 3 位数字（位数为奇数）  
2 是 1 位数字（位数为奇数） 
6 是 1 位数字 位数为奇数） 
7896 是 4 位数字（位数为偶数）  
因此只有 12 和 7896 是位数为偶数的数字
示例 2：

输入：nums = [555,901,482,1771]
输出：1 
解释： 
只有 1771 是位数为偶数的数字。
 

提示：

1 <= nums.length <= 500
1 <= nums[i] <= 10^5


```
//思路1：由于题目很简单，思路也比较清晰，可以先将数字转成字符串然后用字符串的长度判断即可
//思路2：log以10为底去计算num的出来的数字+1即为位数，效率会比转换成字符串效率高，也是判断一个数字位数比较好的计算方法
//思路3：因为直接给出了范围，直接用范围去判断对于这个题目也是可以的，但是不推荐

    public int findNumbers(int[] nums) {
        int count = 0;
        for (Integer num : nums) {
            if (String.valueOf(num).length() % 2 == 0) {
                count++;
            }
        }
        return count;   
    }
```
# 16.1323.6和9组成的最大数字

给你一个仅由数字 6 和 9 组成的正整数 num。

你最多只能翻转一位数字，将 6 变成 9，或者把 9 变成 6 。

请返回你可以得到的最大数字。

 

示例 1：

输入：num = 9669
输出：9969
解释：
改变第一位数字可以得到 6669 。
改变第二位数字可以得到 9969 。
改变第三位数字可以得到 9699 。
改变第四位数字可以得到 9666 。
其中最大的数字是 9969 。
示例 2：

输入：num = 9996
输出：9999
解释：将最后一位从 6 变到 9，其结果 9999 是最大的数。
示例 3：

输入：num = 9999
输出：9999
解释：无需改变就已经是最大的数字了。
 

提示：

1 <= num <= 10^4
num 每一位上的数字都是 6 或者 9 。
```
    //思路： 替换第一个数字为9
    public int maximum69Number (int num) {
     String str = String.valueOf(num);
     str = str.replaceFirst("6", "9");
     return Integer.valueOf(str);  
    }
```

# 17.1266.访问所有点的最小时间

平面上有 n 个点，点的位置用整数坐标表示 points[i] = [xi, yi]。请你计算访问所有这些点需要的最小时间（以秒为单位）。

你可以按照下面的规则在平面上移动：

每一秒沿水平或者竖直方向移动一个单位长度，或者跨过对角线（可以看作在一秒内向水平和竖直方向各移动一个单位长度）。
必须按照数组中出现的顺序来访问这些点。
 

示例 1：



输入：points = [[1,1],[3,4],[-1,0]]
输出：7
解释：一条最佳的访问路径是： [1,1] -> [2,2] -> [3,3] -> [3,4] -> [2,3] -> [1,2] -> [0,1] -> [-1,0]   
从 [1,1] 到 [3,4] 需要 3 秒 
从 [3,4] 到 [-1,0] 需要 4 秒
一共需要 7 秒
示例 2：

输入：points = [[3,2],[-2,2]]
输出：5
 

提示：

points.length == n
1 <= n <= 100
points[i].length == 2
-1000 <= points[i][0], points[i][1] <= 1000


```
    public int minTimeToVisitAllPoints(int[][] points) {
        //思路：根据画图得知，两点之间的距离由，两个点的x的差值和y的差值比较大的决定，
        // 因为要按照数组顺序进行计算距离，所以，遍历所有点分别求出各个点之间的距离后相加
        int startX = points[0][0];
        int startY = points[0][1];
        int disance = 0;
        for (int i = 1; i < points.length; i++) {
            disance += Math.max(Math.abs(points[i][0] - startX), Math.abs(points[i][1] - startY));
            startX = points[i][0];
            startY = points[i][1];
        }
        return disance;

    }
```
# 18.1290.二进制链表转整数

给你一个单链表的引用结点 head。链表中每个结点的值不是 0 就是 1。已知此链表是一个整数数字的二进制表示形式。

请你返回该链表所表示数字的 十进制值 。

 

示例 1：



输入：head = [1,0,1]
输出：5
解释：二进制数 (101) 转化为十进制数 (5)
示例 2：

输入：head = [0]
输出：0
示例 3：

输入：head = [1]
输出：1
示例 4：

输入：head = [1,0,0,1,0,0,1,1,1,0,0,0,0,0,0]
输出：18880
示例 5：

输入：head = [0,0]
输出：0
 

提示：

链表不为空。
链表的结点总数不超过 30。
每个结点的值不是 0 就是 1。
```
    public int getDecimalValue(ListNode head) {
        ListNode node = head;
        int result = 0;
        while (node != null) {
            result = (result << 1) + node.val;
            node = node.next;
        }
        return result;        
    }
```
# 19.1221.分割平衡字符串

在一个「平衡字符串」中，'L' 和 'R' 字符的数量是相同的。

给出一个平衡字符串 s，请你将它分割成尽可能多的平衡字符串。

返回可以通过分割得到的平衡字符串的最大数量。

 
示例 1：

输入：s = "RLRRLLRLRL"
输出：4
解释：s 可以分割为 "RL", "RRLL", "RL", "RL", 每个子字符串中都包含相同数量的 'L' 和 'R'。
示例 2：

输入：s = "RLLLLRRRLR"
输出：3
解释：s 可以分割为 "RL", "LLLRRR", "LR", 每个子字符串中都包含相同数量的 'L' 和 'R'。
示例 3：

输入：s = "LLLLRRRR"
输出：1
解释：s 只能保持原样 "LLLLRRRR".
 

提示：

1 <= s.length <= 1000
s[i] = 'L' 或 'R'

```
    public int balancedStringSplit(String s) {
        int count = 0;
        int result = 0;
        char[] chars = s.toCharArray();
        for (int i = 0; i < chars.length; i++) {
            if (String.valueOf(chars[i]).equals("R")) {
                count++;
            } else {
                count--;
            }
            if (count == 0) {
                result++;
            }
        }
        return result;
    }
```


# 20.226.翻转二叉树

翻转一棵二叉树。

示例：

输入：

     4
   /   \
  2     7
 / \   / \
1   3 6   9
输出：

     4
   /   \
  7     2
 / \   / \
9   6 3   1

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/invert-binary-tree

```
    //思路：从根节点向下一次交换左右节点就可以翻转这棵树
    public TreeNode invertTree(TreeNode root) {
        if(root == null){
            return null;
        }
        //交换节点
        TreeNode temp;
        temp = root.left;
        root.left = root.right;
        root.right = temp;
        if (root.left != null) {
            invertTree(root.left);
        }
        if (root.right != null) {
            invertTree(root.right);
        }
        return root;
        }
```
# 21.938.二叉搜索树的范围和

给定二叉搜索树的根结点 root，返回 L 和 R（含）之间的所有结点的值的和。

二叉搜索树保证具有唯一的值。

 

示例 1：

输入：root = [10,5,15,3,7,null,18], L = 7, R = 15
输出：32
示例 2：

输入：root = [10,5,15,3,7,13,18,1,null,6], L = 6, R = 10
输出：23
 

提示：

树中的结点数量最多为 10000 个。
最终的答案保证小于 2^31。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/range-sum-of-bst

```
    public int rangeSumBST(TreeNode root, int L, int R) {
        if (root == null) {
            return 0;
        }
        int result = 0;
        if (root.val >= L && root.val <= R) {
            //累加结果并向下查找合适的值
            result = root.val + rangeSumBST(root.left, L, R) + rangeSumBST(root.right, L, R);
        } else if (root.val < L) {
            //往子树的右边查找
            return rangeSumBST(root.right,L,R);
        }else {
            //往子树的左边查找
            return rangeSumBST(root.left,L,R);
        }
        return result;        
    }
```



# 22.1304.和为零的N个唯一整数

给你一个整数 n，请你返回 任意 一个由 n 个 各不相同 的整数组成的数组，并且这 n 个数相加和为 0 。


示例 1：

输入：n = 5
输出：[-7,-1,1,3,4]
解释：这些数组也是正确的 [-5,-1,1,2,3]，[-3,-1,2,-2,4]。
示例 2：

输入：n = 3
输出：[-1,0,1]
示例 3：

输入：n = 1
输出：[0]
 

提示：

1 <= n <= 1000

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/find-n-unique-integers-sum-up-to-zero

```
    public int[] sumZero(int n) {
        //思路 在循环中一直添加相反数，如果是奇数个的话就将最后一个赋值为0
        int[] result = new int[n];
        for (int i = 0; i < n; i++) {
            if (i % 2 == 0) {
                result[i] = i + 1;
            } else {
                result[i] = -i;

            }
        }
        if (n % 2 != 0) {
            result[n - 1] = 0;
        }
        return result;
    }


```

# 23.728.自除数

自除数 是指可以被它包含的每一位数除尽的数。

例如，128 是一个自除数，因为 128 % 1 == 0，128 % 2 == 0，128 % 8 == 0。

还有，自除数不允许包含 0 。

给定上边界和下边界数字，输出一个列表，列表的元素是边界（含边界）内所有的自除数。

示例 1：

输入： 
上边界left = 1, 下边界right = 22
输出： [1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 12, 15, 22]
注意：

每个输入参数的边界满足 1 <= left <= right <= 10000。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/self-dividing-numbers

```
    public List<Integer> selfDividingNumbers(int left, int right) {
        List<Integer> ans = new ArrayList();
        for (int n = left; n <= right; ++n) {
            if (selfDividing(n)) ans.add(n);
        }
        return ans;
    }
    public boolean selfDividing(int n) {
        for (char c: String.valueOf(n).toCharArray()) {
            if (c == '0' || (n % (c - '0') > 0))
                return false;
        }
        return true;
    }

```
# 24.804.唯一摩尔斯密码词

国际摩尔斯密码定义一种标准编码方式，将每个字母对应于一个由一系列点和短线组成的字符串， 比如: "a" 对应 ".-", "b" 对应 "-...", "c" 对应 "-.-.", 等等。

为了方便，所有26个英文字母对应摩尔斯密码表如下：

[".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."]
给定一个单词列表，每个单词可以写成每个字母对应摩尔斯密码的组合。例如，"cab" 可以写成 "-.-..--..."，(即 "-.-." + "-..." + ".-"字符串的结合)。我们将这样一个连接过程称作单词翻译。

返回我们可以获得所有词不同单词翻译的数量。

例如:
输入: words = ["gin", "zen", "gig", "msg"]
输出: 2
解释: 
各单词翻译如下:
"gin" -> "--...-."
"zen" -> "--...-."
"gig" -> "--...--."
"msg" -> "--...--."

共有 2 种不同翻译, "--...-." 和 "--...--.".
 

注意:

单词列表words 的长度不会超过 100。
每个单词 words[i]的长度范围为 [1, 12]。
每个单词 words[i]只包含小写字母。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/unique-morse-code-words
```
//思路：使用hashset进行排重，剩下的就是结果
    private static String[] map = {
        ".-",
        "-...",
        "-.-.",
        "-..",
        ".",
        "..-.",
        "--.",
        "....",
        "..",
        ".---",
        "-.-",
        ".-..",
        "--",
        "-.",
        "---",
        ".--.",
        "--.-",
        ".-.",
        "...",
        "-",
        "..-",
        "...-",
        ".--",
        "-..-",
        "-.--",
        "--.."
        };
    public int uniqueMorseRepresentations(String[] words) {
        if (words == null) return 0;
        HashSet<String> set = new HashSet<String>();
        for (String s : words) {
            StringBuilder sb = new StringBuilder();
            for (char c : s.toCharArray()) {
                sb.append(map[c - 'a']);
            }
            set.add(sb.toString());
        }
        return set.size();
    } 

```

# 25.1299.将每个元素替换为右侧最大元素

给你一个数组 arr ，请你将每个元素用它右边最大的元素替换，如果是最后一个元素，用 -1 替换。

完成所有替换操作后，请你返回这个数组。

 

示例：

输入：arr = [17,18,5,4,6,1]
输出：[18,6,6,6,1,-1]
 

提示：

1 <= arr.length <= 10^4
1 <= arr[i] <= 10^5

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/replace-elements-with-greatest-element-on-right-side

```
    public int[] replaceElements(int[] arr) {
        int max = arr[arr.length - 1];
        arr[arr.length - 1] = -1;
        for (int i = arr.length - 2; i >= 0; i--) {
            int temp = arr[i];
            arr[i] = max;
            if (temp > max) max = temp;
            
        }
        return arr;
    }
```

# 26 476.数字的补数

给定一个正整数，输出它的补数。补数是对该数的二进制表示取反。

注意:

给定的整数保证在32位带符号整数的范围内。
你可以假定二进制数不包含前导零位。
示例 1:

输入: 5
输出: 2
解释: 5的二进制表示为101（没有前导零位），其补数为010。所以你需要输出2。
示例 2:

输入: 1
输出: 0
解释: 1的二进制表示为1（没有前导零位），其补数为0。所以你需要输出0。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/number-complement




```
    public int findComplement(int num) {
        //通过异或运算
        int temp = num;
        int temp2 = 1;
        while (temp > 0) {
            temp >>= 1;
            temp2 <<= 1;
        }
        temp2 -= 1;
        return num ^ temp2;
    }
```

# 27.942. 增减字符串匹配

给定只含 "I"（增大）或 "D"（减小）的字符串 S ，令 N = S.length。

返回 [0, 1, ..., N] 的任意排列 A 使得对于所有 i = 0, ..., N-1，都有：

如果 S[i] == "I"，那么 A[i] < A[i+1]
如果 S[i] == "D"，那么 A[i] > A[i+1]
 

示例 1：

输出："IDID"
输出：[0,4,1,3,2]
示例 2：

输出："III"
输出：[0,1,2,3]
示例 3：

输出："DDI"
输出：[3,2,0,1]
 

提示：

1 <= S.length <= 1000
S 只包含字符 "I" 或 "D"。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/di-string-match


```
//思路： 通过观察可以确定的是最大值可以设置为string的长度，最小值为0
遇到'I'就增长一个，遇到'D'就减小一个就可以得到所需要的数组

    public int[] diStringMatch(String s) {
        int length = s.length();
        int max = length;
        int min = 0;
        int[] result = new int[length + 1];
        for (int i = 0; i < length; i++) {
            if (s.charAt(i) == 'I') {
                result[i] = min++;
            } else {
                result[i] = max--;
            }
        }
        result[length] = min;
        return result;
    }
```

# 28.206.反转链表

反转一个单链表。

示例:

输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
进阶:
你可以迭代或递归地反转链表。你能否用两种方法解决这道题？

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/reverse-linked-list
```
        //定义翻转链表的头结点
        ListNode pre = null;
        ListNode current = head;
        //定义临时结点
        ListNode temp = current.next;
        while (current != null) {
            //让当前节点指向上一个节点
            current.next = pre;
            //pre 节点往前走一个节点
            pre = current;
            //current节点也往前走一个节点
            current = temp;
        }
        //返回翻转后的链表的头结点
        return pre;
```
# 29.146.LRU缓存机制

运用你所掌握的数据结构，设计和实现一个  LRU (最近最少使用) 缓存机制。它应该支持以下操作： 获取数据 get 和 写入数据 put 。

获取数据 get(key) - 如果密钥 (key) 存在于缓存中，则获取密钥的值（总是正数），否则返回 -1。
写入数据 put(key, value) - 如果密钥不存在，则写入其数据值。当缓存容量达到上限时，它应该在写入新数据之前删除最近最少使用的数据值，从而为新的数据值留出空间。

进阶:

你是否可以在 O(1) 时间复杂度内完成这两种操作？

示例:

LRUCache cache = new LRUCache( 2 /* 缓存容量 */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // 返回  1
cache.put(3, 3);    // 该操作会使得密钥 2 作废
cache.get(2);       // 返回 -1 (未找到)
cache.put(4, 4);    // 该操作会使得密钥 1 作废
cache.get(1);       // 返回 -1 (未找到)
cache.get(3);       // 返回  3
cache.get(4);       // 返回  4

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/lru-cache


```
    class LRUCache extends LinkedHashMap<Integer,Integer> {
        private  int capacity;
        public LRUCache(int capacity) {
            super(capacity,0.75f,true);
            this.capacity = capacity;
        }

        public int get(int key) {
          return super.getOrDefault(key,-1);
        }

        public void put(int key, int value) {
        super.put(key,value);
        }

    @Override
    protected boolean removeEldestEntry(Map.Entry<Integer, Integer> eldest) {
        return size() > capacity; 
    }

    }
```
# 30.349.两个数组的交集

给定两个数组，编写一个函数来计算它们的交集。

示例 1:

输入: nums1 = [1,2,2,1], nums2 = [2,2]
输出: [2]
示例 2:

输入: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出: [9,4]
说明:

输出结果中的每个元素一定是唯一的。
我们可以不考虑输出结果的顺序。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/intersection-of-two-arrays

```
    public int[] intersection(int[] nums1, int[] nums2) {

    HashSet<Integer> set1 = new HashSet<Integer>();
    for (Integer n : nums1) set1.add(n);
    HashSet<Integer> set2 = new HashSet<Integer>();
    for (Integer n : nums2) set2.add(n);

    set1.retainAll(set2);

    int [] output = new int[set1.size()];
    int idx = 0;
    for (int s : set1) output[idx++] = s;
    return output;

    }
```
# 31.961.重复N次的元素

在大小为 2N 的数组 A 中有 N+1 个不同的元素，其中有一个元素重复了 N 次。

返回重复了 N 次的那个元素。

 

示例 1：

输入：[1,2,3,3]
输出：3
示例 2：

输入：[2,1,2,5,3,2]
输出：2
示例 3：

输入：[5,1,5,2,5,3,5,4]
输出：5
 

提示：

4 <= A.length <= 10000
0 <= A[i] < 10000
A.length 为偶数

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/n-repeated-element-in-size-2n-array

```
    //思路比较简单，如果是数组中一半的元素都是相同的数字，那么无论怎么排列都会有一组连续三个数字其中有两个是相同的，如果没有就是最后两个
    public int repeatedNTimes(int[] A) {
        for (int i = 0; i < A.length - 2; i++) {
            if (A[i] == A[i + 1] || A[i] == A[i + 2]) {
                return A[i];
            }
        }
        return A[A.length - 1];
    }
```
# 32.977.有序数组的平方

给定一个按非递减顺序排序的整数数组 A，返回每个数字的平方组成的新数组，要求也按非递减顺序排序。

 

示例 1：

输入：[-4,-1,0,3,10]
输出：[0,1,9,16,100]
示例 2：

输入：[-7,-3,2,3,11]
输出：[4,9,9,49,121]
 

提示：

1 <= A.length <= 10000
-10000 <= A[i] <= 10000
A 已按非递减顺序排序。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/squares-of-a-sorted-array

```
        public static int[] sortedSquares(int[] nums) {
        //双指针法，声明首位两个指针，然后判断平方的大小再插入新的数组中
        int start = 0;
        int length = nums.length;
        int end = length - 1;
        int[] result = new int[length];
        for (int i = 0; i < length ; i++) {
                if (nums[start] * nums[start] > nums[end] * nums[end]) {
                    result[length - i - 1] = nums[start] * nums[start++];
                } else  {
                    result[length - i - 1] = nums[end] * nums[end--];
                }

        }
        return result;
    }
```

# 33.509.斐波那契数

斐波那契数，通常用 F(n) 表示，形成的序列称为斐波那契数列。该数列由 0 和 1 开始，后面的每一项数字都是前面两项数字的和。也就是：

F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
给定 N，计算 F(N)。

 

示例 1：

输入：2
输出：1
解释：F(2) = F(1) + F(0) = 1 + 0 = 1.
示例 2：

输入：3
输出：2
解释：F(3) = F(2) + F(1) = 1 + 1 = 2.
示例 3：

输入：4
输出：3
解释：F(4) = F(3) + F(2) = 2 + 1 = 3.
 

提示：

0 ≤ N ≤ 30

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/fibonacci-number


```
    public int fib(int num) {
        if (num == 0 || num == 1) {
            return num;
        } else {
            return fib(num - 1) + fib(num - 2);
        }
    }
```

# 34.160.相交链表
编写一个程序，找到两个单链表相交的起始节点。

如下面的两个链表：



在节点 c1 开始相交。

 

示例 1：



输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
输出：Reference of the node with value = 8
输入解释：相交节点的值为 8 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。
 

示例 2：



输入：intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
输出：Reference of the node with value = 2
输入解释：相交节点的值为 2 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [0,9,1,2,4]，链表 B 为 [3,2,4]。在 A 中，相交节点前有 3 个节点；在 B 中，相交节点前有 1 个节点。
 

示例 3：



输入：intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
输出：null
输入解释：从各自的表头开始算起，链表 A 为 [2,6,4]，链表 B 为 [1,5]。由于这两个链表不相交，所以 intersectVal 必须为 0，而 skipA 和 skipB 可以是任意值。
解释：这两个链表不相交，因此返回 null。
 

注意：

如果两个链表没有交点，返回 null.
在返回结果后，两个链表仍须保持原有的结构。
可假定整个链表结构中没有循环。
程序尽量满足 O(n) 时间复杂度，且仅用 O(1) 内存。

来源：力扣（LeetCode）/题目中有图片可以参考链接
链接：https://leetcode-cn.com/problems/intersection-of-two-linked-lists

```
/**
     * 1-2-3-4-5-6-7
     *     |
     *     8
     * 如上两个相交的链表，如果相交那么分辨用两个指针，当指针1从A的头开始走，走到尾的时候接上B的头继续走，如果相交则指针也会相交
     * 有点像赛跑，两人路程一样，速度一样，如果有焦点，那么必定有一段路程是一起走的
     * */
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode p1 = headA;
        ListNode p2 = headB;
        while (p1 != p2) {
            p1 = p1==null?p2:p1.next;
            p2 = p2==null?p1:p2.next;
        }

        return p1;
    }
```
# 35.21.合并两个有序链表
将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

示例：

输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/merge-two-sorted-lists

```
//采用递归的方式进行拼接
 public ListNode mergeTwoLists(ListNode l1, ListNode l2) {

        if(l1 == null) {
            return l2;
        }
        if(l2 == null) {
            return l1;
        }

        if(l1.val < l2.val) {
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        } else {
            l2.next = mergeTwoLists(l1, l2.next);
            return l2;
        }
           
    }
```
# 36.22.链表中倒数第k个节点
输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。例如，一个链表有6个节点，从头节点开始，它们的值依次是1、2、3、4、5、6。这个链表的倒数第3个节点是值为4的节点。

 

示例：

给定一个链表: 1->2->3->4->5, 和 k = 2.

返回链表 4->5.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof

```
//思路：比较蠢想了两个，一个是先测量出来链表长度，返回长度-k的那段链表，另一个是翻转链表然后正着数k个然后再翻转回来
其实最简单的是双指针算法，指定两个指针，让其中一个先走K步，直到为null的这段就是结果
虽然蠢但是也通过了时间复杂度O(N)
    public ListNode getKthFromEnd(ListNode head, int k) {
        ListNode temp = head;
        ListNode result = null;
        int index = 1;
        while (temp.next != null) {
            temp = temp.next;
            index++;
        }
        if(index == k){
            return head;
        }
        for (int i = 0; i < index - k; i++) {
            result = head.next;
            head = head.next;
        }
        return result;        
    }
```
# 37.70.爬楼梯
假设你正在爬楼梯。需要 n 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

注意：给定 n 是一个正整数。

示例 1：

输入： 2
输出： 2
解释： 有两种方法可以爬到楼顶。
1.  1 阶 + 1 阶
2.  2 阶
示例 2：

输入： 3
输出： 3
解释： 有三种方法可以爬到楼顶。
1.  1 阶 + 1 阶 + 1 阶
2.  1 阶 + 2 阶
3.  2 阶 + 1 阶

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/climbing-stairs

```
//思路：此题使用递归会超时，故采用动态规划，使用数组存储每一级台阶的可能性
//爬楼梯 到达第n层，可以分解为到达第n-1层和到达第n-2层之和也就是
// p(n) = p(n-1)+p(n-2)，因为楼梯的走法有走一步和走两步这种。

    public int climbStairs(int n) {
        //递归
        if (n == 1) {
            return 1;
        }
        if (n == 2) {
            return 2;
        }

        return climbStairs(n - 1) + climbStairs(n - 2);
    }


    public int climbStairs(int n) {
        //动态规划
       if (n == 1) {
            return 1;
        }
        if (n == 2) {
            return 2;
        }
        int[] dp = new int[n + 1];
        dp[1] = 1;
        dp[2] = 2;
        for (int i = 3; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
```
# 38.面试题01.01.判定字符是否唯一
实现一个算法，确定一个字符串 s 的所有字符是否全都不同。

示例 1：

输入: s = "leetcode"
输出: false 
示例 2：

输入: s = "abc"
输出: true
限制：

0 <= len(s) <= 100
如果你不使用额外的数据结构，会很加分。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/is-unique-lcci

```
    public boolean isUnique(String str) {
        char[] chars = str.toCharArray();
        for (int i = 0; i < chars.length; i++) {
            if (str.indexOf(String.valueOf(chars[i])) != str.lastIndexOf(String.valueOf(chars[i]))){
                return false;
            }
        }
        return true;        
    }
```
# 39.面试题01.02.判定是否互为字符重排

给定两个字符串 s1 和 s2，请编写一个程序，确定其中一个字符串的字符重新排列后，能否变成另一个字符串。

示例 1：

输入: s1 = "abc", s2 = "bca"
输出: true 
示例 2：

输入: s1 = "abc", s2 = "bad"
输出: false
说明：

0 <= len(s1) <= 100
0 <= len(s2) <= 100

```
//思路:转成数组后排序然后再对比字符串，相等则为true
//也可以转成数组，循环来判断是否相等
    public boolean CheckPermutation(String s1, String s2) {
        char[] chars1 = s1.toCharArray();
        char[] chars2 = s2.toCharArray();
        Arrays.sort(chars1);
        Arrays.sort(chars2);
    return String.valueOf(chars1).equals(String.valueOf(chars2));
    }
```