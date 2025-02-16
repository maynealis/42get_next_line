# Get Next Line

`get_next_line` is a C function that reads text from a file descriptor line by line, without requiring the entire file to be loaded into memory. This project is part of the 42 School curriculum and focuses on static variables, memory management and file handling efficiently.

**Table of contents**
- [Features](#Feautres)
- [How it works](#How-it-works)
- [What I learned](#What-I-learned)


## Features:

- Line-by-line Reading: Returns one line at a time from a file descriptor
- Multiple File Support: Can read from up to 1024 different files simultaneously (bonus part)
- Memory Efficient: Dynamic memory allocation with proper cleanup
- Configurable Buffer: Buffer size can be defined at compilation time
- Error Handling: Robust error management for various edge cases
- No Memory Leaks: Complete memory management with proper cleanup

## 🔍 How it works

Buffer Management:
- A static buffer maintains the leftover characters between function calls.
- For the bonus part, an array of static buffers handles multiple file descriptors.

Reading Process:

- The function reads from the file descriptor using a defined buffer size.
- Content is accumulated until a newline character is found or eof.
- The line is extracted and returned, with remaining content saved for the next call.

Memory Handling:

- Dynamic memory allocation for buffers and string operations.
- Careful memory cleanup in case of errors.
- Proper freeing of resources when no longer needed.


flowchart TD
    A[get_next_line called] --> B{Check fd and BUFFER_SIZE}
    B -->|Invalid| C[Return NULL]
    B -->|Valid| D[Allocate buffer]
    D --> E[Call get_line]
    
    subgraph get_line process
    E --> F{Check static left buffer}
    F -->|Empty| G[Read from fd]
    F -->|Has content| H[Use existing content]
    G --> I[Add to temporary buffer]
    H --> I
    I --> J{Contains newline?}
    J -->|No| G
    J -->|Yes| K[Return complete line]
    end
    
    K --> L[Extract line until \n]
    L --> M[Store remaining in static left]
    M --> N[Clean up memory]
    N --> O[Return line]
    
    subgraph Memory Management
    P[cleanup_memory function]
    P --> Q[Free static left]
    P --> R[Free buffer]
    P --> S[Free line_read]
    P --> T[Free line]
    end
    
    

## 🧠 What I Learned

1. Static Variables:
	- Understanding persistence between function calls
	- Managing state in C functions
	- Handling multiple instances with static arrays

2. Memory Management:
	- Dynamic allocation with malloc
	- Proper memory cleanup to prevent leaks
	- Buffer management and string manipulation

3. File Operations:
	- Working with file descriptors
	- Understanding read operations and buffer sizes
	- Handling I/O errors and edge cases

4. String Manipulation:
	- Implementing custom string functions
	- Efficient string joining and substring operations
	- Buffer overflow prevention

4. Code Organization:
	- Separating utility functions
	- Creating maintainable and reusable code
	- Implementing bonus features without duplicating code


## References

## Project structure

Main Function: get_next_line

Handles file reading and line extraction
Manages static buffer for subsequent calls
Returns complete lines or NULL on errors/EOF


Utility Functions:

ft_strlen: String length calculation
ft_strdup: String duplication
ft_substr: Substring extraction
ft_strjoin: String concatenation


Helper Functions:

cleanup_memory: Memory management and cleanup
index_endline: Newline character detection
get_line: Buffer reading and line accumulation
