# C++ Junior Level Interview Questions

<details>
<summary><h2>#1 Basic Class Implementation [Junior]</h2></summary>

## Problem Statement

Create a simple `Rectangle` class that represents a rectangle with width and height. The class should include:
- Private member variables for width and height
- A constructor that initializes these variables
- Methods to calculate area and perimeter
- Getter and setter methods for width and height

## Template Code

```cpp
// TODO: Implement Rectangle class

int main() {
    Rectangle rect(5, 3);
    std::cout << "Width: " << rect.getWidth() << std::endl;
    std::cout << "Height: " << rect.getHeight() << std::endl;
    std::cout << "Area: " << rect.area() << std::endl;
    std::cout << "Perimeter: " << rect.perimeter() << std::endl;
    
    rect.setWidth(10);
    rect.setHeight(6);
    std::cout << "New Area: " << rect.area() << std::endl;
    std::cout << "New Perimeter: " << rect.perimeter() << std::endl;
    
    return 0;
}
```

## Expected Solution

```cpp
class Rectangle {
private:
    double width;
    double height;
    
public:
    Rectangle(double w, double h) : width(w), height(h) {}
    
    double getWidth() const { return width; }
    double getHeight() const { return height; }
    
    void setWidth(double w) { width = w; }
    void setHeight(double h) { height = h; }
    
    double area() const { return width * height; }
    double perimeter() const { return 2 * (width + height); }
};

// Time Complexity: O(1) for all methods
// Space Complexity: O(1)
```

## Evaluation Criteria

- Proper encapsulation with private member variables
- Correct implementation of constructor and methods
- Use of const correctness for accessor methods
- Proper implementation of getters and setters

</details>

<details>
<summary><h2>#2 Function Overloading [Junior]</h2></summary>

## Problem Statement

Implement a set of overloaded functions named `findMax` that:
1. Finds the maximum of two integers
2. Finds the maximum of three integers
3. Finds the maximum value in an array of integers

## Template Code

```cpp
#include <iostream>

// TODO: Implement three versions of findMax

int main() {
    // Test case 1: Two integers
    std::cout << "Max of 5 and 7: " << findMax(5, 7) << std::endl;
    
    // Test case 2: Three integers
    std::cout << "Max of 3, 9, and 4: " << findMax(3, 9, 4) << std::endl;
    
    // Test case 3: Array of integers
    int arr[] = {12, 45, 67, 23, 9};
    int size = sizeof(arr) / sizeof(arr[0]);
    std::cout << "Max in array: " << findMax(arr, size) << std::endl;
    
    return 0;
}
```

## Expected Solution

```cpp
// Two integers version
int findMax(int a, int b) {
    return (a > b) ? a : b;
}

// Three integers version
int findMax(int a, int b, int c) {
    return findMax(findMax(a, b), c);
}

// Array version
int findMax(int arr[], int size) {
    if (size <= 0) {
        throw std::invalid_argument("Array size must be positive");
    }
    
    int max = arr[0];
    for (int i = 1; i < size; i++) {
        if (arr[i] > max) {
            max = arr[i];
        }
    }
    return max;
}

// Time Complexity: O(1) for first two functions, O(n) for array version
// Space Complexity: O(1) for all functions
```

## Evaluation Criteria

- Proper function overloading with different parameter lists
- Correct implementation of each function
- Error handling for invalid inputs
- Reuse of code where appropriate

</details>

<details>
<summary><h2>#3 Pass By Reference vs Value [Junior]</h2></summary>

## Problem Statement

Implement two functions: `swapByValue` and `swapByReference`. Both should take two integer parameters, but:
- `swapByValue` should swap the values using pass-by-value (and return the swapped values)
- `swapByReference` should swap the values using pass-by-reference

Demonstrate the difference between these two approaches.

## Template Code

```cpp
#include <iostream>

// TODO: Implement swapByValue and swapByReference functions

int main() {
    int a = 5, b = 10;
    
    std::cout << "Before swapByValue: a = " << a << ", b = " << b << std::endl;
    swapByValue(a, b);
    std::cout << "After swapByValue: a = " << a << ", b = " << b << std::endl;
    
    std::cout << "Before swapByReference: a = " << a << ", b = " << b << std::endl;
    swapByReference(a, b);
    std::cout << "After swapByReference: a = " << a << ", b = " << b << std::endl;
    
    return 0;
}
```

## Expected Solution

```cpp
#include <utility> // for std::pair

// Pass by value - won't affect original variables
std::pair<int, int> swapByValue(int a, int b) {
    int temp = a;
    a = b;
    b = temp;
    return std::make_pair(a, b);
}

// Pass by reference - will modify original variables
void swapByReference(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

// Note: In real code, you might use std::swap(a, b) from the <utility> header
```

## Expected Output

```
Before swapByValue: a = 5, b = 10
After swapByValue: a = 5, b = 10       // Original values unchanged
Before swapByReference: a = 5, b = 10
After swapByReference: a = 10, b = 5   // Values swapped
```

## Evaluation Criteria

- Understanding of pass-by-value vs pass-by-reference
- Correct implementation of both functions
- Proper use of reference parameters
- Understanding that pass-by-value does not modify original variables

</details>

<details>
<summary><h2>#4 Vector Manipulation [Junior]</h2></summary>

## Problem Statement

Implement a function called `processVector` that:
1. Takes a vector of integers
2. Removes all negative numbers
3. Doubles all positive even numbers
4. Returns the modified vector

## Template Code

```cpp
#include <iostream>
#include <vector>

// TODO: Implement processVector function

void printVector(const std::vector<int>& vec) {
    for (int num : vec) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
}

int main() {
    std::vector<int> numbers = {1, -3, 4, -2, 6, 0, 8, -5, 10};
    
    std::cout << "Original vector: ";
    printVector(numbers);
    
    std::vector<int> result = processVector(numbers);
    
    std::cout << "Processed vector: ";
    printVector(result);
    
    return 0;
}
```

## Expected Solution

```cpp
#include <vector>

std::vector<int> processVector(const std::vector<int>& vec) {
    std::vector<int> result;
    
    for (int num : vec) {
        if (num < 0) {
            // Skip negative numbers
            continue;
        } else if (num > 0 && num % 2 == 0) {
            // Double positive even numbers
            result.push_back(num * 2);
        } else {
            // Keep other numbers as is
            result.push_back(num);
        }
    }
    
    return result;
}

// Time Complexity: O(n) where n is the size of the input vector
// Space Complexity: O(n) for the result vector
```

## Expected Output

```
Original vector: 1 -3 4 -2 6 0 8 -5 10
Processed vector: 1 8 12 0 16 20
```

## Evaluation Criteria

- Proper handling of the vector data structure
- Correct implementation of the specified operations
- Efficient iteration through the vector
- Correct return of the modified vector

</details>

<details>
<summary><h2>#5 String Manipulation [Junior]</h2></summary>

## Problem Statement

Write a function called `countWordFrequency` that takes a string of text and returns a map where:
- Keys are unique words in the text (case-insensitive)
- Values are the frequencies (number of occurrences) of each word

For this exercise, a "word" is defined as any sequence of alphabetic characters.

## Template Code

```cpp
#include <iostream>
#include <string>
#include <map>

// TODO: Implement countWordFrequency function

void printWordFrequency(const std::map<std::string, int>& wordFreq) {
    for (const auto& pair : wordFreq) {
        std::cout << pair.first << ": " << pair.second << std::endl;
    }
}

int main() {
    std::string text = "The quick brown fox jumps over the lazy dog. The dog was not very lazy.";
    
    std::map<std::string, int> result = countWordFrequency(text);
    
    std::cout << "Word frequencies:" << std::endl;
    printWordFrequency(result);
    
    return 0;
}
```

## Expected Solution

```cpp
#include <string>
#include <map>
#include <cctype>
#include <algorithm>

std::map<std::string, int> countWordFrequency(const std::string& text) {
    std::map<std::string, int> wordFreq;
    std::string currentWord;
    
    for (char c : text) {
        if (std::isalpha(c)) {
            // Add letter to current word (convert to lowercase)
            currentWord += std::tolower(c);
        } else if (!currentWord.empty()) {
            // End of word reached, increment count
            wordFreq[currentWord]++;
            currentWord.clear();
        }
    }
    
    // Check for the last word if text doesn't end with non-alpha character
    if (!currentWord.empty()) {
        wordFreq[currentWord]++;
    }
    
    return wordFreq;
}

// Time Complexity: O(n log m) where n is length of text and m is number of unique words
// Space Complexity: O(m) where m is number of unique words
```

## Expected Output

```
Word frequencies:
brown: 1
dog: 2
fox: 1
jumps: 1
lazy: 2
not: 1
over: 1
quick: 1
the: 2
very: 1
was: 1
```

## Evaluation Criteria

- Proper handling of case-insensitivity
- Correct word boundary detection
- Appropriate use of the map data structure
- Handling of punctuation and special characters

</details>

<details>
<summary><h2>#6 File I/O [Junior]</h2></summary>

## Problem Statement

Implement a program that:
1. Reads numbers from an input file (one integer per line)
2. Calculates the sum, average, minimum, and maximum values
3. Writes the results to an output file

## Template Code

```cpp
#include <iostream>
#include <fstream>
#include <vector>
#include <limits>

// TODO: Implement file reading, statistics calculation, and file writing

int main() {
    std::string inputFileName = "input.txt";
    std::string outputFileName = "output.txt";
    
    // For testing, create the input file with sample data
    {
        std::ofstream testInput(inputFileName);
        testInput << "10\n25\n15\n5\n30\n";
        testInput.close();
    }
    
    bool success = processFile(inputFileName, outputFileName);
    
    if (success) {
        std::cout << "Statistics written to " << outputFileName << std::endl;
        
        // Display the output file contents
        std::ifstream outFile(outputFileName);
        std::string line;
        while (std::getline(outFile, line)) {
            std::cout << line << std::endl;
        }
    } else {
        std::cout << "Failed to process the files." << std::endl;
    }
    
    return 0;
}
```

## Expected Solution

```cpp
#include <iostream>
#include <fstream>
#include <vector>
#include <limits>
#include <numeric> // for std::accumulate
#include <algorithm> // for std::min_element, std::max_element

bool processFile(const std::string& inputFileName, const std::string& outputFileName) {
    std::ifstream inFile(inputFileName);
    if (!inFile) {
        std::cerr << "Error opening input file: " << inputFileName << std::endl;
        return false;
    }
    
    std::vector<int> numbers;
    int num;
    while (inFile >> num) {
        numbers.push_back(num);
    }
    
    if (numbers.empty()) {
        std::cerr << "No numbers found in the input file." << std::endl;
        return false;
    }
    
    // Calculate statistics
    int sum = std::accumulate(numbers.begin(), numbers.end(), 0);
    double average = static_cast<double>(sum) / numbers.size();
    int min = *std::min_element(numbers.begin(), numbers.end());
    int max = *std::max_element(numbers.begin(), numbers.end());
    
    // Write results to output file
    std::ofstream outFile(outputFileName);
    if (!outFile) {
        std::cerr << "Error opening output file: " << outputFileName << std::endl;
        return false;
    }
    
    outFile << "Count: " << numbers.size() << std::endl;
    outFile << "Sum: " << sum << std::endl;
    outFile << "Average: " << average << std::endl;
    outFile << "Minimum: " << min << std::endl;
    outFile << "Maximum: " << max << std::endl;
    
    return true;
}

// Time Complexity: O(n) where n is the number of integers in the file
// Space Complexity: O(n) to store all the numbers
```

## Expected Output in output.txt
```
Count: 5
Sum: 85
Average: 17
Minimum: 5
Maximum: 30
```

## Evaluation Criteria

- Proper file handling and error checking
- Correct calculation of statistics
- Efficient use of appropriate algorithms
- Clean and readable code organization

</details>

<details>
<summary><h2>#7 Exception Handling [Junior]</h2></summary>

## Problem Statement

Implement a function `divideNumbers` that:
1. Takes two integers as parameters
2. Returns their division result as a double
3. Handles potential errors using exception handling:
   - Division by zero
   - Integer overflow/underflow
   - Any other unexpected exceptions

## Template Code

```cpp
#include <iostream>
#include <stdexcept>
#include <limits>

// TODO: Implement divideNumbers function with exception handling

int main() {
    int numerator, denominator;
    
    // Test cases
    std::pair<int, int> testCases[] = {
        {10, 2},           // Normal case
        {5, 0},            // Division by zero
        {std::numeric_limits<int>::max(), 1}, // Large number
        {-5, -2},          // Negative numbers
        {std::numeric_limits<int>::min(), -1} // Potential overflow
    };
    
    for (const auto& test : testCases) {
        numerator = test.first;
        denominator = test.second;
        
        std::cout << "Dividing " << numerator << " by " << denominator << ": ";
        try {
            double result = divideNumbers(numerator, denominator);
            std::cout << "Result = " << result << std::endl;
        }
        catch (const std::exception& e) {
            std::cout << "Exception caught: " << e.what() << std::endl;
        }
    }
    
    return 0;
}
```

## Expected Solution

```cpp
#include <stdexcept>
#include <limits>
#include <string>

double divideNumbers(int numerator, int denominator) {
    // Check for division by zero
    if (denominator == 0) {
        throw std::invalid_argument("Division by zero is not allowed");
    }
    
    // Check for potential overflow (INT_MIN / -1)
    if (numerator == std::numeric_limits<int>::min() && denominator == -1) {
        throw std::overflow_error("Integer overflow in division");
    }
    
    try {
        // Perform division and return result
        return static_cast<double>(numerator) / denominator;
    }
    catch (...) {
        // Catch any other unexpected exceptions
        throw std::runtime_error("Unexpected error occurred during division");
    }
}

// Time Complexity: O(1)
// Space Complexity: O(1)
```

## Expected Output

```
Dividing 10 by 2: Result = 5
Dividing 5 by 0: Exception caught: Division by zero is not allowed
Dividing 2147483647 by 1: Result = 2.14748e+09
Dividing -5 by -2: Result = 2.5
Dividing -2147483648 by -1: Exception caught: Integer overflow in division
```

## Evaluation Criteria

- Proper exception handling for different error cases
- Correct implementation of the division function
- Understanding of numeric limits and potential errors
- Clean structure with appropriate exception types

</details>

<details>
<summary><h2>#8 Simple Inheritance [Junior]</h2></summary>

## Problem Statement

Implement a simple class hierarchy:
1. Create a base class `Vehicle` with:
   - Properties for brand and year
   - A method to display vehicle information
2. Create a derived class `Car` that inherits from `Vehicle` with:
   - Additional property for number of doors
   - An overridden method to display car information

## Template Code

```cpp
#include <iostream>
#include <string>

// TODO: Implement Vehicle and Car classes

int main() {
    Vehicle vehicle("Generic", 2020);
    vehicle.displayInfo();
    
    Car car("Toyota", 2022, 4);
    car.displayInfo();
    
    // Polymorphism test
    Vehicle* vehiclePtr = &car;
    vehiclePtr->displayInfo();
    
    return 0;
}
```

## Expected Solution

```cpp
#include <iostream>
#include <string>

class Vehicle {
protected:
    std::string brand;
    int year;
    
public:
    Vehicle(const std::string& b, int y) : brand(b), year(y) {}
    
    virtual void displayInfo() const {
        std::cout << "Vehicle: " << brand << " (" << year << ")" << std::endl;
    }
    
    // Virtual destructor for proper cleanup in derived classes
    virtual ~Vehicle() {}
};

class Car : public Vehicle {
private:
    int numDoors;
    
public:
    Car(const std::string& b, int y, int doors) : Vehicle(b, y), numDoors(doors) {}
    
    void displayInfo() const override {
        std::cout << "Car: " << brand << " (" << year << "), " 
                  << numDoors << " doors" << std::endl;
    }
};

// Time Complexity: O(1) for all methods
// Space Complexity: O(1)
```

## Expected Output

```
Vehicle: Generic (2020)
Car: Toyota (2022), 4 doors
Car: Toyota (2022), 4 doors
```

## Evaluation Criteria

- Proper implementation of inheritance
- Correct use of virtual functions for polymorphism
- Appropriate member access modifiers (public/protected/private)
- Correct implementation of constructors and destructors

</details>

<details>
<summary><h2>#9 Template Function [Junior]</h2></summary>

## Problem Statement

Implement a template function called `swap` that can exchange the values of any two variables of the same type. Then implement a simple `sort` function that uses your `swap` function to sort an array in ascending order.

## Template Code

```cpp
#include <iostream>

// TODO: Implement swap template function
// TODO: Implement sort function using the swap function

int main() {
    // Test swap with integers
    int a = 5, b = 10;
    std::cout << "Before swap: a = " << a << ", b = " << b << std::endl;
    swap(a, b);
    std::cout << "After swap: a = " << a << ", b = " << b << std::endl;
    
    // Test swap with strings
    std::string s1 = "Hello", s2 = "World";
    std::cout << "Before swap: s1 = " << s1 << ", s2 = " << s2 << std::endl;
    swap(s1, s2);
    std::cout << "After swap: s1 = " << s1 << ", s2 = " << s2 << std::endl;
    
    // Test sort with an array of integers
    int arr[] = {64, 25, 12, 22, 11};
    int n = sizeof(arr) / sizeof(arr[0]);
    
    std::cout << "Original array: ";
    for (int i = 0; i < n; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
    
    sort(arr, n);
    
    std::cout << "Sorted array: ";
    for (int i = 0; i < n; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
    
    return 0;
}
```

## Expected Solution

```cpp
#include <iostream>

// Template function to swap two values of any type
template <typename T>
void swap(T& a, T& b) {
    T temp = a;
    a = b;
    b = temp;
}

// Function to sort an array using the swap function (simple selection sort)
template <typename T>
void sort(T arr[], int size) {
    for (int i = 0; i < size - 1; i++) {
        int minIndex = i;
        
        // Find the minimum element in the unsorted part
        for (int j = i + 1; j < size; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        
        // Swap the minimum element with the first element of the unsorted part
        if (minIndex != i) {
            swap(arr[i], arr[minIndex]);
        }
    }
}

// Time Complexity: O(1) for swap, O(n²) for sort where n is the size of the array
// Space Complexity: O(1) for both functions
```

## Expected Output

```
Before swap: a = 5, b = 10
After swap: a = 10, b = 5
Before swap: s1 = Hello, s2 = World
After swap: s1 = World, s2 = Hello
Original array: 64 25 12 22 11
Sorted array: 11 12 22 25 64
```

## Evaluation Criteria

- Proper implementation of template function
- Correct swapping of values of different types
- Correct sorting implementation using the swap function
- Understanding of template type parameters

</details>

<details>
<summary><h2>#10 Memory Management [Junior]</h2></summary>

## Problem Statement

Create a simple `DynamicArray` class that:
1. Dynamically allocates an array of integers
2. Manages memory properly (no leaks)
3. Provides methods to:
   - Add elements
   - Get elements by index
   - Get the current size
   - Print all elements

## Template Code

```cpp
#include <iostream>

// TODO: Implement DynamicArray class

int main() {
    DynamicArray arr;
    
    // Add elements
    arr.add(10);
    arr.add(20);
    arr.add(30);
    arr.add(40);
    arr.add(50);
    
    // Print array
    std::cout << "Array contents: ";
    arr.print();
    
    // Get element at index 2
    std::cout << "Element at index 2: " << arr.get(2) << std::endl;
    
    // Get size
    std::cout << "Array size: " << arr.size() << std::endl;
    
    // Ensure memory is properly managed
    {
        DynamicArray temp;
        temp.add(100);
        temp.add(200);
        // temp goes out of scope here, destructor should free memory
    }
    
    // Add more elements to original array
    arr.add(60);
    arr.add(70);
    
    std::cout << "Updated array: ";
    arr.print();
    
    return 0;
}
```

## Expected Solution

```cpp
#include <iostream>

class DynamicArray {
private:
    int* arr;         // Pointer to the dynamically allocated array
    int capacity;     // Maximum capacity of the array
    int currentSize;  // Current number of elements
    
    // Helper function to resize array when capacity is reached
    void resize() {
        int newCapacity = capacity * 2;
        int* newArr = new int[newCapacity];
        
        // Copy existing elements
        for (int i = 0; i < currentSize; i++) {
            newArr[i] = arr[i];
        }
        
        // Delete old array and update pointers/capacity
        delete[] arr;
        arr = newArr;
        capacity = newCapacity;
    }
    
public:
    // Constructor
    DynamicArray() : capacity(5), currentSize(0) {
        arr = new int[capacity];
    }
    
    // Destructor
    ~DynamicArray() {
        delete[] arr;  // Free allocated memory
    }
    
    // Add element to the array
    void add(int element) {
        if (currentSize == capacity) {
            resize();
        }
        arr[currentSize++] = element;
    }
    
    // Get element at specific index
    int get(int index) const {
        if (index < 0 || index >= currentSize) {
            throw std::out_of_range("Index out of bounds");
        }
        return arr[index];
    }
    
    // Get current size
    int size() const {
        return currentSize;
    }
    
    // Print all elements
    void print() const {
        for (int i = 0; i < currentSize; i++) {
            std::cout << arr[i];
            if (i < currentSize - 1) {
                std::cout << ", ";
            }
        }
        std::cout << std::endl;
    }
    
    // Copy constructor (to prevent shallow copying)
    DynamicArray(const DynamicArray& other) : capacity(other.capacity), currentSize(other.currentSize) {
        arr = new int[capacity];
        for (int i = 0; i < currentSize; i++) {
            arr[i] = other.arr[i];
        }
    }
    
    // Assignment operator (to prevent shallow copying)
    DynamicArray& operator=(const DynamicArray& other) {
        if (this != &other) {
            delete[] arr;
            
            capacity = other.capacity;
            currentSize = other.currentSize;
            
            arr = new int[capacity];
            for (int i = 0; i < currentSize; i++) {
                arr[i] = other.arr[i];
            }
        }
        return *this;
    }
};

// Time Complexity: O(1) for add (amortized), O(1) for get and size, O(n) for print
// Space Complexity: O(n) where n is the number of elements
```

## Expected Output

```
Array contents: 10, 20, 30, 40, 50
Element at index 2: 30
Array size: 5
Updated array: 10, 20, 30, 40, 50, 60, 70
```

## Evaluation Criteria

- Proper dynamic memory allocation and deallocation
- Implementation of the Rule of Three (destructor, copy constructor, assignment operator)
- Proper array resizing when capacity is reached
- Error handling for invalid indices
- Clean and readable code

</details>
