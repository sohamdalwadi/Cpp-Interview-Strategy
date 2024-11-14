# Core C++ Concepts Questions

### 1. What is the difference between a pointer and a reference in C++?
**Answer**:  
- **Pointer**: Holds a memory address and can be reassigned.
- **Reference**: Acts as an alias and cannot be reassigned once initialized.

### 2. Explain RAII (Resource Acquisition Is Initialization) in C++.
**Answer**:  
RAII ties resource management (e.g., memory, file handles) to the lifetime of objects. When an object goes out of scope, its destructor frees the resource.

### 3. What are the differences between `std::unique_ptr` and `std::shared_ptr`?
**Answer**:  
- **`std::unique_ptr`**: Exclusive ownership, cannot be copied, but can be moved.
- **`std::shared_ptr`**: Shared ownership, reference-counted, can be copied.

### 4. What are lambda expressions in C++? Provide an example.
**Answer**:  
Lambdas are anonymous functions that can capture variables from the surrounding scope.  
Example:
```cpp
auto add = [](int a, int b) { return a + b; };
std::cout << add(3, 4);  // Output: 7
```

### 5. What is `std::move` and when would you use it?
**Answer**:  
`std::move` casts an object to an rvalue reference, enabling move semantics, which transfers resources rather than copying them.
```
