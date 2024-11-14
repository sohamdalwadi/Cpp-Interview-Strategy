# Practical Problem-Solving Questions

### 1. Implement a Stack using Two Queues
```cpp
#include <iostream>
#include <queue>

class StackUsingQueues {
private:
    std::queue<int> q1, q2;

public:
    void push(int x) {
        q2.push(x);
        while (!q1.empty()) {
            q2.push(q1.front());
            q1.pop();
        }
        std::swap(q1, q2);
    }

    int pop() {
        if (q1.empty()) {
            throw std::out_of_range("Stack is empty");
        }
        int front = q1.front();
        q1.pop();
        return front;
    }

    bool empty() {
        return q1.empty();
    }
};
```

### 2. Reverse a String in Place
```cpp
#include <iostream>
#include <string>

void reverseString(std::string& str) {
    int start = 0, end = str.length() - 1;
    while (start < end) {
        std::swap(str[start], str[end]);
        ++start;
        --end;
    }
}

int main() {
    std::string str = "hello";
    reverseString(str);
    std::cout << str << std::endl;  // Output: "olleh"
    return 0;
}
```

### 3. Merge Two Sorted Arrays
```cpp
#include <vector>
#include <iostream>

std::vector<int> mergeSortedArrays(const std::vector<int>& arr1, const std::vector<int>& arr2) {
    std::vector<int> result;
    int i = 0, j = 0;

    while (i < arr1.size() && j < arr2.size()) {
        if (arr1[i] < arr2[j]) {
            result.push_back(arr1[i]);
            ++i;
        } else {
            result.push_back(arr2[j]);
            ++j;
        }
    }

    while (i < arr1.size()) {
        result.push_back(arr1[i]);
        ++i;
    }

    while (j < arr2.size()) {
        result.push_back(arr2[j]);
        ++j;
    }

    return result;
}
```
