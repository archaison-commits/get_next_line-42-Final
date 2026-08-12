*This project has been created as part of the 42 curriculum by brechied.*

# get_next_line

## Description

`get_next_line` is a 42 project focused on reading from a file descriptor one line at a time.

The goal is to understand how `read()` works with buffers and how to keep unread data between function calls. The function returns the next line each time it is called. Including the `\n` when present.

The function:

	char	*get_next_line(int fd);

## Project Structure

```
.
├── get_next_line.c					#Main get_next_line implementation.
├── get_next_line.h         		#Main function prototypes
├── get_next_line_utils.c			#Helper functions for the mandatory part.
├── get_next_line_bonus.c 			#Bonus get_next_line implementation.
├── get_next_line_bonus.h			#Bonus function prototypes
├── get_next_line_utils_bonus.c		#Helper functions for the Bonus part.
├── README.md

```


## Instructions

- Compile the mandatory part with

	cc -Wall -Wextra -Werror -D BUFFER_SIZE=42 get_next_line.c get_next_line_utils.c

You can change `BUFFER_SIZE` to any positive value.

- For the bonus:

	cc -Wall -Wextra -Werror -D BUFFER_SIZE=42 get_next_line_bonus.c get_next_line_utils_bonus.c

The function can then be used as:

	char	*line;

	line = get_next_line(fd);

## Algorithm

The implementation uses a static `stash` to keep unread data between calls.

1. Read data from the file descriptor into a buffer.
2. Append the buffer to the stash.
3. Continue reading until a `\n` is found or EOF is reached.
4. Extract the first line from the stash.
5. Keep everything after the newline for the next call.
6. Return the extracted line.

The stash grows when more space is needed. Its length and capacity are tracked to reduce unnecessary allocations and copying, especially with small `BUFFER_SIZE` values and large lines.

For the bonus, a separate stash is maintained for each file descriptor.

- Works with different `BUFFER_SIZE` values.
- Handles files with or without a final newline.
- Handles empty files and multiple newlines.
- Handles large lines.
- Proper memory management.
- Bonus supports multiple file descriptors.

## Resources

- `read()` — https://man7.org/linux/man-pages/man2/read.2.html
- `malloc()` — https://man7.org/linux/man-pages/man3/malloc.3.html
- `free()` — https://man7.org/linux/man-pages/man3/free.3p.html
- C reference — https://en.cppreference.com/w/c

## Testing

Tested with:

- `BUFFER_SIZE = 1`
- `BUFFER_SIZE = 42`
- `BUFFER_SIZE = 10000000`
- Empty files
- Large lines
- Multiple lines
- Files with and without `\n`
- `stdin`
- Invalid file descriptors
- Multiple file descriptors (bonus)

### AI usage

AI was used as a learning and testing tool during the project.

It helped me understand `read()`, static variables, dynamic memory, time complexity and different ways of managing the stash. It was also used to investigate compiler errors and performance issues.

The implementation, testing and final decisions were made by the author.




