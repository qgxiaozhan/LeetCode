1. 原题

Given two arrays, write a function to compute their intersection.

Example:
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2, 2].

Note:
- Each element in the result should appear as many times as it shows in both arrays.
- The result can be in any order.

Follow up:
- What if the given array is already sorted? How would you optimize your algorithm?
- What if nums1's size is small compared to nums2's size? Which algorithm is better?
- What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

2. 中文意思
  给定两个数组，返回两个数组中共同的部分，需要注意是如果都有多个，需要返回多个。


3. 第一篇解法，利用 hashMap ， 可以AC，但是只打败了8%
```
public class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {

        Map<Integer, Integer> nums1Map = new HashMap<Integer, Integer>();
        Map<Integer, Integer> nums2Map = new HashMap<Integer, Integer>();

        for (int num : nums1){
            if (nums1Map.containsKey(num)){
                nums1Map.put(num, nums1Map.get(num) + 1);
            }else {
                nums1Map.put(num, 1);
            }
        }

        for (int num : nums2){
            if (nums2Map.containsKey(num)){
                nums2Map.put(num, nums2Map.get(num) + 1);
            }else {
                nums2Map.put(num, 1);
            }
        }

        List<Integer> numList = new LinkedList<Integer>();
        for (int key : nums1Map.keySet()){
            if (nums2Map.containsKey(key)){
                int time = Math.min(nums1Map.get(key), nums2Map.get(key));
                for (int i = 0; i < time; i ++){
                    numList.add(key);
                }
            }
        }

        int [] result = new int[numList.size()];
        int index = 0;
        for (int num : numList){
            result[index] = num;
            index ++;
        }
        return result;
    }
}
```
