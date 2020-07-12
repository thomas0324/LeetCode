# LeetCode

#### 2020/07/13
Question: Given an integer array nums, return the sum of divisors of the integers in that array that have exactly four divisors.If there is no such integer in the array, return 0. 

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

[Reference](https://leetcode.com/problems/four-divisors/)
 
 
