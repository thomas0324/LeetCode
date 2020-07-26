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

    Definition of a complete binary tree from Wikipedia:
        In a complete binary tree every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between         1 and 2h nodes inclusive at the last level h.
    
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
