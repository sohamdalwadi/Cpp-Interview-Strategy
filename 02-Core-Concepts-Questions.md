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

#### **Lambdas**
- **What are lambda expressions and when would you use them?**
  - Lambda expressions are anonymous functions that can capture variables from their surrounding scope and are often used in algorithms or functions expecting function pointers or callable objects.
  - Syntax: `[capture](parameters) -> return_type { body }`

#### **Move Semantics and `std::move`**
- **What is move semantics in C++ and how is it implemented?**
  - Move semantics allow resources to be transferred rather than copied, which improves performance (especially for large objects). 
  - The `std::move` function casts an object to an rvalue reference, allowing the transfer of ownership.

#### **`std::unique_ptr` and `std::shared_ptr`**
- **How do `std::unique_ptr` and `std::shared_ptr` help manage memory in C++?**
  - `std::unique_ptr` ensures that only one pointer owns the object at a time and automatically deallocates the memory when it goes out of scope.
  - `std::shared_ptr` allows multiple pointers to share ownership of an object, and it automatically deletes the object when the last shared pointer is destroyed.

#### **`std::optional` and `std::variant`**
- **What is the difference between `std::optional` and `std::variant`?**
  - **`std::optional<T>`** represents a value that may or may not be present. It is used when a value is optional.
  - **`std::variant<T1, T2, ...>`** is a type-safe union that can hold one of several types, providing a way to store and manipulate data of multiple types in a single variable.

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
