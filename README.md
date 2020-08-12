# 2020-8-12
485. 最大连续1的个数
    给定一个二进制数组， 计算其中最大连续1的个数。
    示例 1:
    输入: [1,1,0,1,1,1]
    输出: 3
    解释: 开头的两位和最后的三位都是连续1，所以最大连续1的个数是 3.
    注意：
        输入的数组只包含 0 和1。
        输入数组的长度是正整数，且不超过 10,000。
思路：
    用一个计数器 count 记录 1 的数量，另一个计数器 maxCount 记录当前最大的 1 的数量。
    当我们遇到 1 时，count 加一。
    当我们遇到 0 时：
        将 count 与 maxCount 比较，maxCoiunt 记录较大值。
        将 count 设为 0。
    返回 maxCount。
题解：
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int count = 0;
        int maxCount = 0;
        for(int i = 0;i < nums.length;i++){
            if(nums[i] == 1)
                count++;
            else{
                maxCount = Math.max(maxCount,count);
                count = 0;
            }
        }
        return Math.max(maxCount,count);
    }
}

492. 构造矩形
    作为一位web开发者， 懂得怎样去规划一个页面的尺寸是很重要的。 现给定一个具体的矩形页面面积，你的任务是设计一个长度为 L 和宽度为 W 且满足以下要求的矩形的页面。要求：
    1. 你设计的矩形页面必须等于给定的目标面积。
    2. 宽度 W 不应大于长度 L，换言之，要求 L >= W 。
    3. 长度 L 和宽度 W 之间的差距应当尽可能小。
    你需要按顺序输出你设计的页面的长度 L 和宽度 W。
    示例：
    输入: 4
    输出: [2, 2]
    解释: 目标面积是 4， 所有可能的构造方案有 [1,4], [2,2], [4,1]。
    但是根据要求2，[1,4] 不符合要求; 根据要求3，[2,2] 比 [4,1] 更能符合要求. 所以输出长度 L 为 2， 宽度 W 为 2。
思路：
    对这个数开方，然后往下递减，遇到第一个可以整除的，就是最好的结果，且为宽度
    为什么要开方：题中要求找到L,W最相近的结果，那么最理想的情况是这个数可以开方，L=W，当他不能开方的时候，找到最接近平方根的数应该就是结果
    为什么往下递减第一个可以整除的是宽度：因为L>W
    为什么向下递减：由于int是向下取整，如果选择向上递增的时候会出现问题，如输入2，开方取整后得到1,这里由于直接可以整除了，不会进入到+1那一步，所以L和W会取反，如果向下递减则不需要判断这种边界条件
题解：
    class Solution {
    public int[] constructRectangle(int area) {
        int sqrt = (int) Math.sqrt(area);
        while(area % sqrt != 0)
            sqrt--;
        return new int[]{area / sqrt,sqrt};    
    }
}

496. 下一个更大元素 I
    给定两个 没有重复元素 的数组 nums1 和 nums2 ，其中nums1 是 nums2 的子集。找到 nums1 中每个元素在 nums2 中的下一个比其大的值。
    nums1 中数字 x 的下一个更大元素是指 x 在 nums2 中对应位置的右边的第一个比 x 大的元素。如果不存在，对应位置输出 -1 。
    示例 1:
    输入: nums1 = [4,1,2], nums2 = [1,3,4,2].
    输出: [-1,3,-1]
    解释:
        对于num1中的数字4，你无法在第二个数组中找到下一个更大的数字，因此输出 -1。
        对于num1中的数字1，第二个数组中数字1右边的下一个较大数字是 3。
        对于num1中的数字2，第二个数组中没有下一个更大的数字，因此输出 -1。
思路：
    遍历数组nums1，
    用指针j找到nums1[i]在nums2中的位置，
    从nums1[i]出现之后找到第一个比他大的数然后把nums1中替换为此数，
    找不到替换为-1。
题解:
 class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        for(int i = 0;i < nums1.length;i++){
            int j = 0;
            for(;j < nums2.length;j++){
                if(nums1[i] == nums2[j]){
                    break;
                }
            }
            while(j < nums2.length){
                if(nums2[j] > nums1[i]){
                    nums1[i] = nums2[j];
                    break;
                }else
                    j++;
            }
            if(j == nums2.length)
                nums1[i] = -1;
        }
        return nums1;
    }
}
