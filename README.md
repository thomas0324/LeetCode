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

My Answer: Math

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

Example:

    Given binary tree [3,9,20,null,null,15,7]
    
                                3
                               / \
                              9  20
                                /  \
                               15   7
                               
    Return [[3],[9,20],[15,7]]

My Answer: BFS 

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

#### 2020/07/15
[Question](https://leetcode.com/problems/valid-parentheses/): Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid. An input string is valid if: Open brackets must be closed by the same type of brackets. Open brackets must be closed in the correct order. Note that an empty string is also considered valid.
    
Example:

    Input: "()"
    Output: true
    
    Input: "()[]{}"
    Output: true
    
    Input: "([)]"
    Output: false
 
My Answer: Stack

    class Solution {
        public boolean isValid(String s) {
            Stack<Character> stack = new Stack<Character>();

            if(s.length() % 2 != 0) {
                return false ;
            }

            for(int i = 0 ; i < s.length() ; i++) {
                char temp = s.charAt(i) ;
                switch(temp){
                    case '(' : case '[': case '{': 
                        stack.push(temp) ;
                        break ;
                    case ')':
                        if(stack.size() == 0 || stack.peek() != '(') return false ;
                        else {
                            stack.pop() ;
                            break ;
                        }
                    case ']':
                        if(stack.size() == 0 || stack.peek() != '[' ) return false ;
                        else {
                            stack.pop() ;
                            break ;
                        }
                    case '}':
                        if(stack.size() == 0 || stack.peek() != '{' ) return false ;
                        else {
                            stack.pop() ;
                            break ;
                        }
                }
            }
            return (stack.size() == 0) ? true : false ;    
        }
    }

Time Complexity: O(n) where n is the length of the string

#### 2020/07/17
[Question](https://leetcode.com/problems/robot-return-to-origin/): There is a robot starting at position (0, 0), the origin, on a 2D plane. Given a sequence of its moves, judge if this robot ends up at (0, 0) after it completes its moves. The move sequence is represented by a string, and the character moves[i] represents its ith move. Valid moves are R (right), L (left), U (up), and D (down). If the robot returns to the origin after it finishes all of its moves, return true. Otherwise, return false. Note: The way that the robot is "facing" is irrelevant. "R" will always make the robot move to the right once, "L" will always make it move left, etc. Also, assume that the magnitude of the robot's movement is the same for each move.

Example: 
    
    Input: "UD"
    Output: true 
    Explanation: The robot moves up once, and then down once. All moves have the same magnitude, so it ended up at the origin where it started. Therefore, we           return true.
    
    Input: "LL"
    Output: false
    Explanation: The robot moves left twice. It ends up two "moves" to the left of the origin. We return false because it is not at the origin at the end of its       moves.

My Answer: 
    
    class Solution {
        public boolean judgeCircle(String moves) {

            int x = 0 ;
            int y = 0 ;

            for(int i = 0 ; i < moves.length() ; i++){
                switch(moves.charAt(i)){
                    case 'U':
                        y++;
                        break ;
                    case 'D':
                        y--;
                        break ;
                    case 'L':
                        x-- ;
                        break ;
                    case 'R':
                        x++ ;
                        break ;
                    default:
                        break ;
                }
            }
            return (x == 0 && y == 0)? true : false ;
        }
    }

Time Complexity: O(n) where n is the length of the string

#### 2020/07/26
[Question](https://leetcode.com/problems/count-complete-tree-nodes/): Given a complete binary tree, count the number of nodes.
    
Example
    
    Input: 
            1
           / \
          2   3
         / \  /
        4  5 6

    Output: 6

My Answer:

    class Solution {

        public int counter = 0 ;
        public int countNodes(TreeNode root) {
            return traversal(root) ;
        }

        public int traversal(TreeNode root) {
            if(root == null) {
                return counter ; 
            } else {
                traversal(root.left) ;
                counter ++ ; 
                traversal(root.right) ;
            }
            return counter ; 

        }
    }
    
Time Complexity: O(n) where n is the number of node of the tree

#### 2020/08/16
[Question](https://leetcode.com/problems/maximum-depth-of-binary-tree/): Given a binary tree, find its maximum depth. The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

Example: 

    Given binary tree [3,9,20,null,null,15,7]
            3
           / \
          9  20
            /  \
           15   7
           
    return 3

My Answer:

     /**
     * Definition for a binary tree node.
     * public class TreeNode {
     *     int val;
     *     TreeNode left;
     *     TreeNode right;
     *     TreeNode(int x) { val = x; }
     * }
     */
    class Solution {
        public int maxDepth(TreeNode root) {
            if(root == null) {
                return 0;
            }

            int left = maxDepth(root.left) ;
            int right = maxDepth(root.right) ;

            System.out.println("Now checking on the node " + root.val) ; 

            return Math.max(left,right) + 1 ;

        }
    }

Time Complexity: O(n) where n is the number of node in the tree 

#### 2020/08/17
[Question](https://leetcode.com/explore/featured/card/august-leetcoding-challenge/551/week-3-august-15th-august-21st/3427/): 

We distribute some number of candies, to a row of n = num_people people in the following way:

We then give 1 candy to the first person, 2 candies to the second person, and so on until we give n candies to the last person.

Then, we go back to the start of the row, giving n + 1 candies to the first person, n + 2 candies to the second person, and so on until we give 2 * n candies to the last person.

This process repeats (with us giving one more candy each time, and moving to the start of the row after we reach the end) until we run out of candies.  The last person will receive all of our remaining candies (not necessarily one more than the previous gift).

Return an array (of length num_people and sum candies) that represents the final distribution of candies. 

Example: 
    
    Input: candies = 7, num_people = 4
    Output: [1,2,3,1]
    Explanation:
    On the first turn, ans[0] += 1, and the array is [1,0,0,0].
    On the second turn, ans[1] += 2, and the array is [1,2,0,0].
    On the third turn, ans[2] += 3, and the array is [1,2,3,0].
    On the fourth turn, ans[3] += 1 (because there is only one candy left), and the final array is [1,2,3,1].
    
My Answer:

    class Solution {
        public int[] distributeCandies(int candies, int num_people) {
            int[] people = new int[num_people] ;
            int pointer = 0 ;
            int numberOfCandies = 1 ;

            while(candies != 0) {
                if(candies - numberOfCandies >= 0) {
                    pointer = index(pointer, num_people) ;
                    people[pointer] += numberOfCandies;
                    candies -= numberOfCandies ;
                    numberOfCandies ++ ;
                } else {
                    pointer = index(pointer, num_people) ;
                    numberOfCandies = candies ; 
                    candies = 0 ;
                    people[pointer] += numberOfCandies ; 
                }
                pointer++ ;   
            }
            return people ;
        }

        public int index(int pointer, int num_people) {
            if(pointer == num_people) {
                return 0 ; 
            } else {
                return pointer ;
            }
        }
    }

Time Complexity: O(m) where m is the number of iterations until candies = 0 

#### 2020/08/20
[Question](https://leetcode.com/problems/goat-latin/): 

A sentence S is given, composed of words separated by spaces. Each word consists of lowercase and uppercase letters only.

We would like to convert the sentence to "Goat Latin" (a made-up language similar to Pig Latin.)

The rules of Goat Latin are as follows:

If a word begins with a vowel (a, e, i, o, or u), append "ma" to the end of the word.
For example, the word 'apple' becomes 'applema'.
 
If a word begins with a consonant (i.e. not a vowel), remove the first letter and append it to the end, then add "ma".
For example, the word "goat" becomes "oatgma".
 
Add one letter 'a' to the end of each word per its word index in the sentence, starting with 1.
For example, the first word gets "a" added to the end, the second word gets "aa" added to the end and so on.

Return the final sentence representing the conversion from S to Goat Latin. 

Example: 

    Input: "I speak Goat Latin"
    Output: "Imaa peaksmaaa oatGmaaaa atinLmaaaaa"

My Answer: 

    class Solution {
        public String toGoatLatin(String S) {
            String[] words = S.split("\\W+");
            String a = "a" ;
            String answer = "" ;

            for(int i = 0 ; i < words.length ; i++) {
                System.out.println("Now checking " + words[i]) ;
                if(isVowel(words[i])) {
                    words[i] += "ma" ;
                } else {
                    char first = words[i].charAt(0) ;
                    words[i] = words[i].substring(1) ;
                    words[i] += first ; 
                    words[i] += "ma" ; 
                }

                words[i] = words[i] + a ; 
                a += "a" ;

                if(i != words.length-1) {
                    words[i] += " " ;
                }
                answer += words[i] ;
            }
            return answer ;
        }

        public boolean isVowel(String word) {
            word = word.toLowerCase() ;
            char first = word.charAt(0) ;
            if(first == 'a' || first == 'e' || first == 'i' || first == 'o' || first == 'u') {
                return true ;
            } 
            return false ;
        }
    }

Time Complexity: O(n) where n is the number of words in the String
