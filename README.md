# LeetCode

#### 2020/07/12
[Question](https://leetcode.com/problems/four-divisors/): Given an integer array nums, return the sum of divisors of the integers in that array that have exactly four divisors.If there is no such integer in the array, return 0. 

Example: 

    Input: nums = [21,4,7]
    Output: 32
    
    Explanation:
        21 has 4 divisors: 1, 3, 7, 21
        4 has 3 divisors: 1, 2, 4
        7 has 2 divisors: 1, 7
        The answer is the sum of divisors of 21 only.

My Answer

    class Solution {
        public int sumFourDivisors(int[] nums) {
            int sum = 0 ;
        
            for(int i = 0 ; i < nums.length ; i++) {
                sum += isDivisor(nums[i]) ;
            }
        
            return sum ; 
        }
    
        public static int isDivisor(int num) {
            int num1 = (int)Math.sqrt(num) ;
        
            // check if the number is a square number , if yes, the number will not come up with an even number of divisors 
            if(num1 * num1 == num) {
                return 0 ; 
            }
        
            int sum = 1 + num, counter = 2 ;
 
            for(int i = 2 ; i < Math.sqrt(num) ; i++ ) {
                if(num % i == 0) {
                    int num2 = num / i ; 
                    sum += num2 ;
                    sum += i ; 
                    counter += 2 ; 
                }
            }
            if(counter == 4) {
                return sum ;
            }
            return 0 ;
    }

Time Complexity: O(n*sqrt(m))  where n is the number of element in the array, sqrt(m) is the iteration of the Math.sqrt(num) 
 
#### 2020/07/13
[Question](https://leetcode.com/problems/find-peak-element/): A peak element is an element that is greater than its neighbors. Given an input array nums, where nums[i] ≠ nums[i+1], find a peak element and return its index.The array may contain multiple peaks, in that case return the index to any one of the peaks is fine. You may imagine that nums[-1] = nums[n] = -∞.

Example: 

    Input: nums = [1,2,3,1]
    Output: 2
    Explanation: 3 is a peak element and your function should return the index number 2.
    
    Input: nums = [1,2,1,3,5,6,4]
    Output: 1 or 5 
    Explanation: Your function can return either index number 1 where the peak element is 2, or index number 5 where the peak element is 6.

My Answer: 
    
    class Solution {
        public int findPeakElement(int[] nums) {
        
            for(int i = 1 ; i < nums.length ; i++) {
                if(i != nums.length-1 && nums[i-1] < nums[i] && nums[i] > nums[i+1]) {
                    return i ;
                }
                if(i == nums.length-1 && nums[i] > nums[i-1]) {
                    return i ; 
                }
            }
            return 0 ;    
        }
    }

Time Complexity: O(n) where n is the number of element in the array

#### 2020/07/14 
[Question](https://leetcode.com/problems/binary-tree-level-order-traversal/submissions/): Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:

    Given binary tree [3,9,20,null,null,15,7]
    
                                3
                               / \
                              9  20
                                /  \
                               15   7
                               
    Return [[3],[9,20],[15,7]]

My Answer: 

    class Solution {
        public List<List<Integer>> levelOrder(TreeNode root) {

            if(root == null) {
                return new ArrayList<List<Integer>>() ;
            }

            List<Integer> list = new ArrayList<>() ;
            List<List<Integer>> answer = new ArrayList<List<Integer>>() ;
            Queue<TreeNode> queue = new LinkedList<TreeNode>() ; 

            TreeNode node = root ; 
            queue.add(node) ;
            list.add(node.val) ;
            answer.add(list) ;


            while(queue.size() != 0) {
                list = new ArrayList<>() ;
                int size = queue.size() ;

                for(int i = 0 ; i < size ; i++) {
                    node = queue.remove() ;
                    if(node.left != null) {
                        queue.add(node.left) ;
                        list.add(node.left.val) ;
                    }
                    if(node.right != null) {
                        queue.add(node.right) ;
                        list.add(node.right.val) ;
                    }
                }

                if(list.size() != 0) {
                    answer.add(list) ;
                }
            }
            return answer ; 
        }
    }

Time Complexity: O(n) where n is the number of visited node 

    
                              
