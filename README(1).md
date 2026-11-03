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


## Resources

- `man printf`, `man stdarg`, `man write` - to get to know function behaviour
- 42 Norm (norminette) documentation

### Use of AI

AI was not used in this project
