*This project has been created as part of the 42 curriculum by ekariavk.*

# ft_printf

## Description

`ft_printf` is a re-implementation of the C standard library function `printf()`.
The goal of the project is to learn how **variadic functions** work in C
(`<stdarg.h>`).

The library is built as `libftprintf.a` and implements a function:

```c
int ft_printf(const char *format, ...);
```

It returns the number of characters written, like `printf()`.

### Supported conversions

| Specifier | Output                                         |
|-----------|------------------------------------------------|
| `%c`      | a single character                             |
| `%s`      | a string (`(null)` if the pointer is `NULL`)   |
| `%p`      | a `void *` in hexadecimal, prefixed by `0x` (`(nil)` for `NULL`) |
| `%d`      | a signed decimal integer                       |
| `%i`      | a signed decimal integer                       |
| `%u`      | an unsigned decimal integer                    |
| `%x`      | an unsigned integer in lowercase hexadecimal   |
| `%X`      | an unsigned integer in uppercase hexadecimal   |
| `%%`      | a literal percent sign                         |

### Project layout

| File               | Role                                                   |
|--------------------|--------------------------------------------------------|
| `ft_printf.c`      | format-string parser and conversion dispatcher         |
| `ft_printf.h`      | prototypes                               |
| `ft_putchar_fd.c`  | writes one character and increments the counter        |
| `ft_putstr_fd.c`   | writes a string (handles `NULL`)                       |
| `ft_putnbr_fd.c`   | writes a signed number in base 10                      |
| `ft_putunnbr_fd.c` | writes an unsigned number in base 10                   |
| `ft_puthex.c`      | writes an unsigned number in base 16 (lower/upper)     |
| `ft_putptr_fd.c`   | writes a pointer in hexadecimal                        |
| `ft_strlen.c`      | string length                                 |

## Instructions

### Compilation

```sh
make        # builds libftprintf.a at the root of the repository
make clean  # removes object and dependency files
make fclean # removes objects and libftprintf.a
make re     # fclean + all
```

The project is compiled with `cc -Wall -Wextra -Werror`, and the library is
created with `ar rcs`.

### Usage

Include the header and link against the library:

```c
#include "ft_printf.h"

int main(void)
{
	int n;

	n = ft_printf("Hello %s, you are %d years old (0x%x)\n", "42", 7, 255);
	ft_printf("%d characters were printed\n", n);
	return (0);
}
```
## Algorithm and data structure

**Parsing.** `ft_printf` walks the format string once, from left to right,
with a single index. Every character that is not a `%` is written as is. When a
`%` is found, the next character is examined:

- `%` prints a literal `%`;
- any other character is handed to a dispatcher (`ft_format`), which selects
  the matching conversion;


**Variadic arguments.** A single `va_list` is created with `va_start`, passed
by pointer to the dispatcher, and consumed with `va_arg` using the type that
matches each conversion (`int` for `%c`/`%d`/`%i`, `unsigned int` for
`%u`/`%x`/`%X`, `char *` for `%s`, `void *` for `%p`). Passing the list by
pointer guarantees that the arguments consumed inside the helper are really
consumed for the caller. `va_end` is called before returning.

**Counting output.** No intermediate buffer is used. Each helper writes
directly with `write()` and increments a shared `int *res` counter that is
passed down from `ft_printf`. This keeps the helpers independent, allows the
return value to be computed for free, and follows the subject's rule not to
re-implement the buffering of the original `printf()`.

**Number conversion.** Numbers are printed recursively: the function prints
`n / base` first, then the last digit `n % base`. This produces the digits in
the right order without allocating memory or reversing a buffer. Hexadecimal
digits are looked up in a constant string (`"0123456789abcdef"` or its
uppercase variant). Signed numbers are handled with a `long long`, so the sign
can be flipped safely even for `INT_MIN`.

**Pointers.** `%p` converts the address to an `unsigned long long`, stores its
hexadecimal digits in a small fixed-size array, and prints them after the `0x` prefix. A `NULL` pointer prints `(nil)`, which
matches glibc on Linux.

**Why this design.** The only data structures are the `va_list` and one
integer counter. There is no heap allocation, so there is nothing to free and no
possibility of leaks. Adding a new conversion only requires one helper
function and one extra line in the dispatcher, which keeps the code
extensible.

## Resources

- `man printf`, `man stdarg`, `man write` - to get to know function behaviour
- 42 Norm (norminette) documentation

### Use of AI

AI was not used in this project
