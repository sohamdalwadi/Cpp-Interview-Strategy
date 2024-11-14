# Practical Problem-Solving Questions

This document contains a collection of practical problems that can be used in C++ technical interviews. The problems are categorized by topic, and each section can be expanded as new topics and challenges arise. These problems are designed to assess a candidate's problem-solving skills, knowledge of algorithms and data structures, and understanding of core C++ concepts.

---

### **Array and String Manipulation**

#### **Reverse a String In-Place**
- **Problem**: Write a function that reverses a given string in place (without using additional memory for another string).
- **Example**:
  ```cpp
  std::string str = "hello";
  reverseString(str);
  std::cout << str;  // Output: "olleh"
  ```
- **Solution**:
  ```cpp
  void reverseString(std::string& str) {
      int start = 0, end = str.length() - 1;
      while (start < end) {
          std::swap(str[start], str[end]);
          ++start;
          --end;
      }
  }
  ```

#### **Find Missing Number in Array**
- **Problem**: Given an array of integers from 1 to n, with one number missing, find the missing number.
- **Example**:
  ```cpp
  std::vector<int> arr = {1, 2, 4, 5};
  int missing = findMissingNumber(arr);  // Output: 3
  ```
- **Solution**:
  ```cpp
  int findMissingNumber(const std::vector<int>& arr) {
      int n = arr.size() + 1;
      int sum = (n * (n + 1)) / 2;
      int arr_sum = std::accumulate(arr.begin(), arr.end(), 0);
      return sum - arr_sum;
  }
  ```

#### **Rotate an Array**
- **Problem**: Given an array, rotate the array to the right by k steps.
- **Example**:
  ```cpp
  std::vector<int> arr = {1, 2, 3, 4, 5};
  rotateArray(arr, 2);
  // Output: arr = {4, 5, 1, 2, 3}
  ```
- **Solution**:
  ```cpp
  void rotateArray(std::vector<int>& arr, int k) {
      int n = arr.size();
      k = k % n;  // Handle rotation greater than array size
      std::reverse(arr.begin(), arr.end());
      std::reverse(arr.begin(), arr.begin() + k);
      std::reverse(arr.begin() + k, arr.end());
  }
  ```

---

### **Linked Lists**

#### **Reverse a Linked List**
- **Problem**: Write a function that reverses a singly linked list.
- **Example**:
  ```cpp
  ListNode* head = ...; // linked list with elements 1 -> 2 -> 3
  head = reverseLinkedList(head);
  // Output: Linked list reversed to 3 -> 2 -> 1
  ```
- **Solution**:
  ```cpp
  struct ListNode {
      int val;
      ListNode* next;
      ListNode(int x) : val(x), next(nullptr) {}
  };
  
  ListNode* reverseLinkedList(ListNode* head) {
      ListNode* prev = nullptr;
      ListNode* curr = head;
      while (curr != nullptr) {
          ListNode* next_node = curr->next;
          curr->next = prev;
          prev = curr;
          curr = next_node;
      }
      return prev;
  }
  ```

#### **Detect Cycle in Linked List**
- **Problem**: Write a function to detect if a cycle exists in a singly linked list.
- **Example**:
  ```cpp
  ListNode* head = ...; // linked list
  bool hasCycle = detectCycle(head);
  // Output: true if cycle exists, false otherwise
  ```
- **Solution**:
  ```cpp
  bool detectCycle(ListNode* head) {
      if (!head) return false;
      ListNode* slow = head;
      ListNode* fast = head;
      
      while (fast && fast->next) {
          slow = slow->next;
          fast = fast->next->next;
          if (slow == fast) return true;
      }
      
      return false;
  }
  ```

---

### **Sorting and Searching**

#### **Binary Search**
- **Problem**: Implement binary search on a sorted array to find the index of a target element.
- **Example**:
  ```cpp
  std::vector<int> arr = {1, 2, 3, 4, 5};
  int index = binarySearch(arr, 4);  // Output: 3
  ```
- **Solution**:
  ```cpp
  int binarySearch(const std::vector<int>& arr, int target) {
      int left = 0, right = arr.size() - 1;
      while (left <= right) {
          int mid = left + (right - left) / 2;
          if (arr[mid] == target) return mid;
          else if (arr[mid] < target) left = mid + 1;
          else right = mid - 1;
      }
      return -1;  // Target not found
  }
  ```

#### **Merge Two Sorted Arrays**
- **Problem**: Given two sorted arrays, merge them into one sorted array.
- **Example**:
  ```cpp
  std::vector<int> arr1 = {1, 3, 5};
  std::vector<int> arr2 = {2, 4, 6};
  std::vector<int> merged = mergeSortedArrays(arr1, arr2);
  // Output: merged = {1, 2, 3, 4, 5, 6}
  ```
- **Solution**:
  ```cpp
  std::vector<int> mergeSortedArrays(const std::vector<int>& arr1, const std::vector<int>& arr2) {
      std::vector<int> result;
      int i = 0, j = 0;
      while (i < arr1.size() && j < arr2.size()) {
          if (arr1[i] < arr2[j]) result.push_back(arr1[i++]);
          else result.push_back(arr2[j++]);
      }
      while (i < arr1.size()) result.push_back(arr1[i++]);
      while (j < arr2.size()) result.push_back(arr2[j++]);
      return result;
  }
  ```

---

### **Dynamic Programming**

#### **Fibonacci Sequence (Optimized)**
- **Problem**: Calculate the nth Fibonacci number using dynamic programming with O(n) time and O(1) space.
- **Example**:
  ```cpp
  int n = 10;
  int fib = fibonacci(n);  // Output: 55
  ```
- **Solution**:
  ```cpp
  int fibonacci(int n) {
      if (n <= 1) return n;
      int prev1 = 0, prev2 = 1;
      for (int i = 2; i <= n; ++i) {
          int current = prev1 + prev2;
          prev1 = prev2;
          prev2 = current;
      }
      return prev2;
  }
  ```

#### **Knapsack Problem (0/1 Knapsack)**
- **Problem**: Given weights and values of items, find the maximum value that can be carried in a knapsack of capacity `W`.
- **Example**:
  ```cpp
  std::vector<int> values = {60, 100, 120};
  std::vector<int> weights = {10, 20, 30};
  int capacity = 50;
  int maxValue = knapsack(values, weights, capacity);  // Output: 220
  ```
- **Solution**:
  ```cpp
  int knapsack(const std::vector<int>& values, const std::vector<int>& weights, int capacity) {
      int n = values.size();
      std::vector<std::vector<int>> dp(n + 1, std::vector<int>(capacity + 1, 0));
      
      for (int i = 1; i <= n; ++i) {
          for (int w = 1; w <= capacity; ++w) {
              if (weights[i - 1] <= w) {
                  dp[i][w] = std::max(dp[i - 1][w], dp[i - 1][w - weights[i - 1]] + values[i - 1]);
              } else {
                  dp[i][w] = dp[i - 1][w];
              }
          }
      }
      return dp[n][capacity];
  }
  ```

---

### **Recursion and Backtracking**

#### **Permutations of a String**
- **Problem**: Given a string, return all possible permutations of the string.
- **Example**:
  ```cpp
  std::string str = "abc";
  std::vector<std::string> permutations = getPermutations(str);
  // Output: {"abc", "acb", "bac", "bca", "cab", "cba"}
  ```
- **Solution**:
  ```cpp
  void generatePermutations(std::string& str, int index, std::vector<std::string>& result) {
     

  if (index == str.length()) {
          result.push_back(str);
          return;
      }
      for (int i = index; i < str.length(); ++i) {
          std::swap(str[i], str[index]);
          generatePermutations(str, index + 1, result);
          std::swap(str[i], str[index]);  // backtrack
      }
   }

  std::vector<std::string> getPermutations(std::string str) {
      std::vector<std::string> result;
      generatePermutations(str, 0, result);
      return result;
  }
  ```

---

### **Other Topics**

#### **Graph Traversal (DFS/BFS)**
- **Problem**: Implement Depth First Search (DFS) and Breadth First Search (BFS) on a graph.
  - DFS: Explore as far as possible along each branch before backtracking.
  - BFS: Explore all neighbors of a node before moving to the next level.
