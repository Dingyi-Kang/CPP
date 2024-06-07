In C++, the use of `object->func` versus `object.func` depends on whether `object` is a pointer or an instance (object) of a class.

### Using `object->func`

- **Pointer to an Object:** The `->` operator is used to call a member function or access a member variable through a pointer to an object.

**When to Use:**
- When you have a pointer to an object, you use the `->` operator to access its members (both functions and variables).

**Example:**
```cpp
class MyClass {
public:
    void func() {
        std::cout << "Member function called." << std::endl;
    }
};

int main() {
    MyClass* objPtr = new MyClass(); // objPtr is a pointer to an object of MyClass
    objPtr->func(); // Use -> to call func() on the pointer

    delete objPtr; // Don't forget to delete the dynamically allocated memory
    return 0;
}
```

### Using `object.func`

- **Object (Instance):** The `.` operator is used to call a member function or access a member variable through an instance of a class.

**When to Use:**
- When you have an actual object (not a pointer), you use the `.` operator to access its members (both functions and variables).

**Example:**
```cpp
class MyClass {
public:
    void func() {
        std::cout << "Member function called." << std::endl;
    }
};

int main() {
    MyClass obj; // obj is an instance of MyClass
    obj.func(); // Use . to call func() on the instance

    return 0;
}
```

### Summary of Differences

1. **Pointer to an Object:**
   - **Syntax:** `object->func`
   - **Use Case:** When `object` is a pointer to an object.

2. **Object (Instance):**
   - **Syntax:** `object.func`
   - **Use Case:** When `object` is an instance of a class (not a pointer).

### Example with Both Scenarios

Let's see an example that includes both a pointer to an object and an instance of an object:

```cpp
#include <iostream>

class MyClass {
public:
    void func() {
        std::cout << "Member function called." << std::endl;
    }
};

int main() {
    // Using an instance of the class
    MyClass obj;
    obj.func(); // Calls func() using the . operator

    // Using a pointer to an object of the class
    MyClass* objPtr = new MyClass();
    objPtr->func(); // Calls func() using the -> operator

    delete objPtr; // Clean up dynamically allocated memory
    return 0;
}
```

### Key Points

- **Instance (`.`):** Use the `.` operator when you have a direct instance of the class.
- **Pointer (`->`):** Use the `->` operator when you have a pointer to an instance of the class.
- **Memory Management:** When using pointers, be mindful of memory management, including allocation and deallocation.

By understanding the difference between these two operators and their respective use cases, you can effectively manage and manipulate objects and pointers in C++.
