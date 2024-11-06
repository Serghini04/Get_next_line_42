## 📋 Description

`get_next_line` is a function that reads a line ending with a newline character (`\n`) from a file descriptor. When called repeatedly, it allows reading a text file line by line until the end. This project aims to improve understanding of static variables, memory allocation, and file manipulation in C.

## 🔧 Function Prototype

```c
char *get_next_line(int fd);
```

### Parameters
- `fd`: The file descriptor to read from

### Return Value
- Returns the line that was read (including the newline character unless it's the end of file and doesn't end with a newline)
- Returns NULL if there is nothing else to read or if an error occurred

## ⭐ Features

- 📖 Reads from multiple file descriptors simultaneously
- 🔒 No memory leaks
- 📏 Handles various buffer sizes
- ↩️ Returns one line at a time
- ⌨️ Works with both files and standard input

## 💻 Usage

### 🔨 Compilation

To compile with a specific buffer size:
```bash
cc -Wall -Wextra -Werror -D BUFFER_SIZE=42 get_next_line.c get_next_line_utils.c
```

### 📝 Example

```c
#include "get_next_line.h"
#include <fcntl.h>
#include <stdio.h>

int main(void)
{
    int fd = open("test.txt", O_RDONLY);
    char *line;

    while ((line = get_next_line(fd)) != NULL)
    {
        printf("%s", line);
        free(line);
    }
    close(fd);
    return (0);
}
```

## 📁 Files

- `get_next_line.c`: Main function implementation
- `get_next_line.h`: Header file with function prototypes and includes
- `get_next_line_utils.c`: Helper functions
- `get_next_line_bonus.c`: Bonus part implementation (multiple fd handling)
- `get_next_line_utils_bonus.c`: Bonus helper functions

## ⚙️ Requirements

- The function should return the line that was read
- If there is nothing else to read or if an error occurred, it should return NULL
- The returned line should include the terminating `\n` character except if the end of file was reached and does not end with a `\n`
- Works with any BUFFER_SIZE value greater than 0

## 📌 Notes

- External functions allowed: read, malloc, free
- All memory allocated with malloc must be properly freed
- Undefined behavior if the file pointed to by the file descriptor changed since the last call whereas read() didn't reach the end of file
- Undefined behavior when reading a binary file
