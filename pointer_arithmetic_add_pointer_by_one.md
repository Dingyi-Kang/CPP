The reason `cur_node_coords.get() + 1` refers to the second element of the array instead of the second byte after the pointer `cur_node_coords.get()` is because of how pointer arithmetic works in C++.

### Pointer Arithmetic in C++

When you perform arithmetic operations on pointers in C++, the compiler automatically adjusts the pointer by the size of the type it points to. This means that adding `1` to a pointer does not increase the pointer value by `1` byte, but by `sizeof(T)` bytes, where `T` is the type of the elements in the array.

### Explanation with Example

Let's break it down with a concrete example:

1. **Array and Pointer Initialization:**

   ```cpp
   std::unique_ptr<int[]> cur_node_coords = std::make_unique<int[]>(3);
   cur_node_coords[0] = 1;
   cur_node_coords[1] = 2;
   cur_node_coords[2] = 3;
   ```

   Here, `cur_node_coords` is a `std::unique_ptr` managing an array of `int` with 3 elements.

2. **Pointer Arithmetic:**

   ```cpp
   int* ptr = cur_node_coords.get();
   ```

   - `ptr` now points to the first element of the array, `1`.

   ```cpp
   ptr + 1;
   ```

   - Adding `1` to `ptr` does not increment the pointer by `1` byte but by `sizeof(int)` bytes. Assuming `sizeof(int) = 4` bytes, `ptr + 1` actually points to `ptr + 4` in memory, which is the second element of the array, `2`.

### How Pointer Arithmetic Works

- **Base Address Calculation:**
  - Let's assume `cur_node_coords.get()` returns a pointer with address `0x1000` (just an example).
  - The array looks like this in memory:
    ```
    Address    Value
    0x1000     1
    0x1004     2
    0x1008     3
    ```

- **Incrementing the Pointer:**
  - When you do `ptr + 1`, the compiler calculates the new address as `0x1000 + 1 * sizeof(int)`.
  - Given `sizeof(int) = 4` bytes, the new address becomes `0x1000 + 4 = 0x1004`, which points to the second element, `2`.

### Code Example

Here's a complete code example demonstrating this:

```cpp
#include <iostream>
#include <memory>

int main() {
    // Allocate and initialize the array
    std::unique_ptr<int[]> cur_node_coords = std::make_unique<int[]>(3);
    cur_node_coords[0] = 1;
    cur_node_coords[1] = 2;
    cur_node_coords[2] = 3;

    // Get the raw pointer to the array
    int* ptr = cur_node_coords.get();

    // Print the values using pointer arithmetic
    std::cout << "First element: " << *ptr << std::endl;          // Output: 1
    std::cout << "Second element: " << *(ptr + 1) << std::endl;   // Output: 2
    std::cout << "Third element: " << *(ptr + 2) << std::endl;    // Output: 3

    return 0;
}
```

### Summary

- **Pointer Arithmetic:** Increments and decrements pointers by the size of the type they point to, not by bytes.
- **Element Access:** `cur_node_coords.get() + 1` points to the second element of the array because `1` is multiplied by `sizeof(T)`, where `T` is the type of the array elements.
- **Type Size Adjustment:** The compiler handles the necessary adjustments based on the size of the type the pointer points to, ensuring correct element access in arrays.
