## Summary:

std::string filename: Passes a copy of the string, useful when you need a local copy.

const char *filename: A pointer to a constant C-style string, used for compatibility with C code.

const std::string &filename: A constant reference to a string, efficient and prevents modification of the original string.

## Use Cases:
Use std::string when you need to manipulate a local copy of the string or when interacting purely within C++.

Use const char * for interfacing with C libraries or legacy code that uses C-style strings.

Use const std::string & for efficient read-only access to a string without copying.
