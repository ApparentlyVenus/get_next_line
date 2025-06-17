# get_next_line - Line Reading Function ✔️ 100/100

A function that reads and returns one line at a time from a file descriptor, handling multiple files simultaneously with efficient memory management.

## 📖 About

get_next_line is a project that implements a function to read text files line by line. This is particularly useful for processing large files without loading them entirely into memory.

## ✨ Features

- **Line-by-Line Reading**: Read one line at a time from any file descriptor
- **Memory Efficient**: Uses minimal memory with configurable buffer size
- **EOF Handling**: Proper end-of-file detection and handling
- **Error Management**: Robust error handling for various edge cases
- **Configurable Buffer**: Customizable buffer size via compilation flags

## 🚀 Function Prototype

```c
char *get_next_line(int fd);
```

**Parameters**: 
- `fd` - File descriptor to read from

**Returns**: 
- The next line from the file (including `\n` if present)
- `NULL` when end of file is reached or on error

## 🛠️ Compilation

```bash
# Basic compilation
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=1024 get_next_line.c get_next_line_utils.c

# With custom buffer size
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 get_next_line.c get_next_line_utils.c

```

## 📦 Usage Examples

### Basic File Reading
```c
#include "get_next_line.h"
#include <fcntl.h>
#include <stdio.h>

int main(void)
{
    int fd;
    char *line;
    
    fd = open("example.txt", O_RDONLY);
    if (fd == -1)
        return (1);
    
    while ((line = get_next_line(fd)) != NULL)
    {
        printf("%s", line);
        free(line);
    }
    
    close(fd);
    return (0);
}
```

### Reading from Standard Input
```c
#include "get_next_line.h"
#include <stdio.h>

int main(void)
{
    char *line;
    
    printf("Enter text (Ctrl+D to end):\n");
    while ((line = get_next_line(0)) != NULL)  // 0 = stdin
    {
        printf("You entered: %s", line);
        free(line);
    }
    
    return (0);
}
```

## 🏗️ Project Structure

### Mandatory Version
```
get_next_line/
├── get_next_line.c         # Main function implementation
├── get_next_line_utils.c   # Helper functions
├── get_next_line.h         # Header file
└── README.md               # This file
```

## ⚙️ Configuration

### Buffer Size
The buffer size can be configured at compile time:

```bash
# Small buffer (good for testing)
gcc -D BUFFER_SIZE=1 ...

# Medium buffer (balanced)
gcc -D BUFFER_SIZE=1024 ...

# Large buffer (faster for big files)
gcc -D BUFFER_SIZE=8192 ...
```

**Buffer Size Effects**:
- **Small buffers** (1-10): More system calls, slower but uses less memory
- **Medium buffers** (1024-4096): Balanced performance and memory usage
- **Large buffers** (8192+): Fewer system calls, faster but uses more memory
