# Core C++ Concepts Questions

This document contains a set of core C++ concepts questions designed to assess a candidate's understanding of fundamental and advanced topics in C++. These questions are grouped by category, and you can add new sections or questions as needed.

---

### **Memory Management**

#### **Pointers and References**
- **What is the difference between a pointer and a reference in C++?**
  - **Pointers** store memory addresses and can be reassigned to point to different objects or `nullptr`. They can be dereferenced using `*`.
  - **References** are aliases for another variable. Once initialized, a reference cannot be made to refer to a different object. They cannot be `nullptr` and do not require dereferencing.
  
#### **Dynamic Memory Management**
- **How does memory allocation and deallocation work in C++?**
  - Use `new` and `delete` to allocate and free memory manually, but these can lead to memory leaks if not handled properly. 
  - Modern C++ prefers using **smart pointers** (`std::unique_ptr`, `std::shared_ptr`) to automate memory management and prevent leaks.

#### **Smart Pointers**
- **What is the difference between `std::unique_ptr` and `std::shared_ptr`?**
  - **`std::unique_ptr`** is for exclusive ownership of an object, ensuring that only one `unique_ptr` can own the object at a time.
  - **`std::shared_ptr`** allows multiple shared owners, where the object is deleted when the last `shared_ptr` pointing to it goes out of scope.
  
- **What is a `std::weak_ptr` and when would you use it?**
  - A `std::weak_ptr` is a non-owning smart pointer that allows you to observe an object managed by `std::shared_ptr` without extending its lifetime. It helps avoid **circular references** in cases where two or more objects need to reference each other.

#### **RAII (Resource Acquisition Is Initialization)**
- **Can you explain RAII and how it is implemented in C++?**
  - RAII ties the lifetime of resources (memory, file handles, sockets, etc.) to the lifetime of objects. In C++, this is usually implemented through smart pointers or custom classes with destructors that clean up resources.

---

### **Object-Oriented Programming (OOP)**

#### **Classes and Objects**
- **What are the key principles of Object-Oriented Programming in C++?**
  - **Encapsulation**: Wrapping data and functions into a single unit (class) and restricting access to the internal state using access specifiers (`private`, `protected`, `public`).
  - **Inheritance**: Deriving new classes from existing ones to promote code reuse and extend functionality.
  - **Polymorphism**: Allowing objects of different classes to be treated as objects of a common base class, enabling flexibility and dynamic behavior.
  - **Abstraction**: Hiding complex implementation details and exposing only the necessary interface to the user.

#### **Constructors and Destructors**
- **What is the role of constructors and destructors in C++?**
  - **Constructors** are special member functions that are invoked when an object is created to initialize its state.
  - **Destructors** are called when an object is destroyed to clean up resources (e.g., memory deallocation).
  - C++ also supports **copy constructors** and **move constructors** to control the behavior of object copying and moving.

#### **Inheritance**
- **How is inheritance implemented in C++?**
  - C++ supports both **single** and **multiple inheritance**. A derived class can inherit from one or more base classes and extend or override their functionality.
  - Access specifiers (`private`, `protected`, `public`) determine the visibility of inherited members.
  
#### **Virtual Functions and Polymorphism**
- **What is polymorphism and how does it work in C++?**
  - Polymorphism in C++ is achieved using **virtual functions**. A base class declares a virtual function, and derived classes override it. This enables dynamic dispatch at runtime (i.e., the correct function is called based on the object type, not the pointer or reference type).

---

### **C++11/14/17/20 Features**

# Core Concepts - C++11/14/17/20 Features

#### **Lambdas**
- **What are lambda expressions and when would you use them?**
  - **C++11**: Lambda expressions are anonymous functions that can capture variables from their surrounding scope and are often used in algorithms or functions expecting function pointers or callable objects.
  - **Syntax**: `[capture](parameters) -> return_type { body }`
  - **Example**:
    ```cpp
    auto add = [](int x, int y) { return x + y; };
    std::cout << add(3, 4);  // Outputs: 7
    ```
  - **Use case**: Lambdas are commonly used in standard algorithms (e.g., `std::sort`, `std::for_each`), where passing a function object is needed but defining a separate function would be cumbersome.

- **What is the difference between capturing by reference and by value in lambdas?**
  - **C++11**: A lambda can capture variables either by reference or by value:
    - **Capture by reference** (`&`): The lambda accesses the original variable, and any modifications affect the captured variable outside the lambda.
    - **Capture by value** (`=`): The lambda copies the value of the variable at the time of the capture, and changes inside the lambda do not affect the original variable.
  - **Example**:
    ```cpp
    int a = 5, b = 10;
    auto lambda_ref = [&a, b](int x) { return a + b + x; };
    auto lambda_val = [a, b](int x) { return a + b + x; };
    a = 15;
    std::cout << lambda_ref(5);  // Outputs: 30 (a is modified)
    std::cout << lambda_val(5);  // Outputs: 20 (a is not modified)
    ```

- **What are generic lambdas introduced in C++14?**
  - **C++14**: C++14 allows lambdas to be more generic by enabling the use of `auto` in the parameter list. This allows lambdas to work with any type of argument.
  - **Syntax**: `[capture](auto param1, auto param2) { return param1 + param2; }`
  - **Example**:
    ```cpp
    auto add = [](auto x, auto y) { return x + y; };
    std::cout << add(3, 4);     // Outputs: 7
    std::cout << add(3.5, 4.5); // Outputs: 8.0
    ```

- **What are lambdas with template parameters introduced in C++20?**
  - **C++20**: In C++20, lambdas can have template parameters, allowing for even more flexibility. This allows lambdas to be type-generic and behave like template functions.
  - **Syntax**: `[]<typename T>(T x, T y) { return x + y; }`
  - **Example**:
    ```cpp
    auto add = []<typename T>(T x, T y) { return x + y; };
    std::cout << add(3, 4);    // Outputs: 7 (int)
    std::cout << add(3.5, 4.5); // Outputs: 8.0 (double)
    ```

---

#### **Auto Keyword**
- **What is the purpose of the `auto` keyword in C++11?**
  - **C++11**: The `auto` keyword is used to automatically deduce the type of a variable from its initializer. It simplifies code, especially when dealing with complex iterator types or template-based code.
  - **Example**:
    ```cpp
    auto x = 10;  // x is of type int
    auto y = 3.14; // y is of type double
    std::vector<int>::iterator iter = vec.begin();
    auto iter2 = vec.begin();  // auto deduces iterator type
    ```

- **What is `auto`'s role in function return type deduction in C++14?**
  - **C++14**: C++14 introduces return type deduction for functions using the `auto` keyword. This allows the compiler to automatically deduce the return type of the function.
  - **Example**:
    ```cpp
    auto add(int a, int b) { return a + b; } // return type deduced as int
    std::cout << add(3, 4);  // Outputs: 7
    ```

---

#### **Range-based for Loop**
- **What is a range-based for loop and how does it improve code readability in C++11?**
  - **C++11**: The range-based for loop provides a simpler way to iterate over containers without needing explicit iterators or index-based access. It automatically iterates over the elements of a container.
  - **Syntax**: `for (auto& element : container) { // code }`
  - **Example**:
    ```cpp
    std::vector<int> vec = {1, 2, 3, 4};
    for (auto& num : vec) {
        std::cout << num << " ";  // Outputs: 1 2 3 4
    }
    ```

---

#### **Move Semantics and Rvalue References**
- **What are rvalue references and how do they enable move semantics in C++11?**
  - **C++11**: Rvalue references (denoted by `&&`) allow you to distinguish between lvalues (objects that persist) and rvalues (temporary objects). This is useful for **move semantics**, which enables the transfer of resources (like dynamically allocated memory) from temporary objects to new objects, without copying.
  - **Syntax**: `T&&`
  - **Example**:
    ```cpp
    class MyClass {
    public:
        MyClass(std::vector<int>&& data) : data_(std::move(data)) {}  // Move constructor
    private:
        std::vector<int> data_;
    };
    std::vector<int> vec = {1, 2, 3};
    MyClass obj(std::move(vec));  // Moves the vector into MyClass
    ```

- **How does the `std::move` function work in move semantics?**
  - **C++11**: `std::move` is used to cast an object to an rvalue reference, enabling move semantics.
  - **Example**:
    ```cpp
    std::vector<int> vec = {1, 2, 3};
    std::vector<int> vec2 = std::move(vec);  // Moves resources from vec to vec2
    ```

---

#### **Smart Pointers**
- **What are smart pointers and how do they differ from regular pointers?**
  - **C++11**: Smart pointers are wrappers around raw pointers that automatically manage the memory they point to. They prevent memory leaks by ensuring that memory is freed when no longer needed.
  - **Types**:
    - **`std::unique_ptr`**: Owns a resource exclusively (no shared ownership).
    - **`std::shared_ptr`**: Allows shared ownership of a resource.
    - **`std::weak_ptr`**: Non-owning reference to a `shared_ptr`, used to avoid circular references.
  - **Example**:
    ```cpp
    std::unique_ptr<int> ptr = std::make_unique<int>(5);
    std::shared_ptr<int> ptr2 = std::make_shared<int>(10);
    ```

---

#### **`constexpr`**
- **What is `constexpr` in C++11 and later, and how does it affect performance?**
  - **C++11**: `constexpr` is used to define functions and variables that can be evaluated at compile time. This helps in optimizing performance by reducing runtime computations.
  - **Example**:
    ```cpp
    constexpr int square(int x) { return x * x; }
    int arr[square(10)];  // Size is computed at compile-time
    ```

- **How did `constexpr` evolve in C++14 and C++17?**
  - **C++14**: Allowed more complex expressions inside `constexpr` functions, including loops and `if` statements.
  - **C++17**: Introduced **`if constexpr`**, which allows conditional compilation based on constant expressions.
  - **Example**:
    ```cpp
    template <typename T>
    void print(T value) {
        if constexpr (std::is_integral<T>::value) {
            std::cout << "Integer: " << value;
        } else {
            std::cout << "Other type: " << value;
        }
    }
    ```

---

#### **Structured Bindings (C++17)**
- **What are structured bindings in C++17?**
  - **C++17**: Structured bindings allow unpacking tuple-like objects (e.g., `std::pair`, `std::tuple`) into individual variables. This improves code readability and simplifies working with such types.
  - **Example**:
    ```cpp
    std::pair<int, std::string> p = {1, "Hello"};
    auto [x, y] = p;  // Unpacks the pair into x = 1 and y = "Hello"
    std::cout << x << ", " << y;  // Outputs: 1, Hello
    ```

---

#### **Concepts (C++20)**
- **What are Concepts in C++20, and how do they improve template programming?**
  - **C++20**: Concepts allow specifying constraints on template parameters. This makes template code more readable and easier to understand by providing more expressive error messages and ensuring that only types satisfying certain conditions are passed to templates.
  - **Example**:
    ```cpp
    template <typename T>
    concept Addable = requires(T a, T b) { a + b; };

    template <Addable T>
    T add(T a, T b) {
        return a + b;
    }

    std::cout << add(3, 4);  // Works for integers
    ```

---

### **Templates and Metaprogramming**

#### **Template Basics**
- **How do templates work in C++?**
  - Templates allow the definition of generic types, functions, or classes. They enable type-safe and reusable code.
  - C++ supports **function templates** and **class templates**, both of which allow for parameterized types.

#### **Template Specialization**
- **What is template specialization and why would you use it?**
  - **Template specialization** is used to define different behavior for specific types or values. This allows you to create custom implementations for particular data types.

#### **SFINAE (Substitution Failure Is Not An Error)**
- **What is SFINAE and how is it useful in C++?**
  - SFINAE allows you to enable or disable template instantiation based on certain conditions (e.g., the presence of a member function or a valid type).
  - It's often used with **`std::enable_if`** to create highly flexible, type-safe code.

---

### **Concurrency and Multithreading**

#### **Threading in C++**
- **What are the basics of threading in C++?**
  - The **`std::thread`** class allows you to create and manage threads in C++. Threads run concurrently and can execute functions or callable objects in parallel.

#### **Mutexes and Locks**
- **What is the role of mutexes in multithreading?**
  - **Mutexes** (`std::mutex`) are used to ensure that only one thread can access shared data at a time, preventing **data races** and **race conditions**.
  - `std::lock_guard` and `std::unique_lock` provide automatic locking and unlocking of mutexes, making them safer to use in complex code.

#### **Condition Variables**
- **How do condition variables work in C++?**
  - **Condition variables** (`std::condition_variable`) are used to synchronize threads by allowing one thread to wait for another thread to notify it that a certain condition has been met.

---

### **Advanced C++ Concepts**

#### **C++20 Features**
- **What new features were introduced in C++20?**
  - Some notable features include **concepts** (for constraining template types), **ranges** (for working with sequences), **coroutines** (for asynchronous programming), and **`std::format`** (for string formatting).

#### **Operator Overloading**
- **What is operator overloading, and how do you overload operators in C++?**
  - **Operator overloading** allows you to define custom behavior for operators (e.g., `+`, `-`, `*`) when they are used with user-defined types. You can overload operators as member functions or non-member functions.

#### **Type Traits and `std::is_*`**
- **What are type traits in C++?**
  - Type traits are a collection of template structures that provide information about types at compile time. For example, `std::is_integral<T>` checks whether a type is an integral type.
  - These can be used to enable or disable template instantiations based on type properties.

---

### **Best Practices and Code Design**

#### **Exception Handling**
- **How does exception handling work in C++?**
  - C++ uses `try`, `catch`, and `throw` to handle exceptions. Exceptions allow for separation of error-handling code from normal logic.
  - Proper exception handling ensures the robustness of code, especially in resource management (e.g., RAII).

#### **Rule of Three/Five**
- **What is the Rule of Three/Five in C++?**
  - The **Rule of Three** states that if a class needs to implement a **destructor**, **copy constructor**, or **copy assignment operator**, it should likely implement all three.
  - The **Rule of Five** extends this to include the **move constructor** and **move assignment operator** for efficient resource management in modern C++.

---

### **Other C++ Concepts**
- **Namespaces**
- **Preprocessor Directives**
- **Static vs. Dynamic Linking**
- **C++ Standard Library (STL) Containers**: `std::vector`, `std::list`, `std::map`, etc.

---

This document can easily be updated or expanded with new topics as the field of C++ evolves. Each section is designed to be flexible so that you can add new concepts, questions, and answers as your interviews progress.
