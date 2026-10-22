*This project has been created as part of the 42 curriculum by ekariavk.*

# Libft — your very first own library

## Description

**Goal.** `libft` is a static C library that re-implements a set of the most frequently used functions of the C standard library (`libc`) under the `ft_` prefix.

**Overview.** The project is written from scratch. The functions of the first part may not call any external function at all (only \malloc`/`free` where allocation is explicitly required), the code follows the 42 Norm and compiles with `-Wall -Wextra -Werror`.

What it is **not**: it does not aim for the exact byte-level behaviour of every libc implementation. It implements what the man pages specify, including the well-defined edge cases that a copy-paste programmer never notices (overlapping buffers in `memmove`, `size == 0` in `strlcpy`, `NULL` terminator search in `strnstr`, `nmemb == 0` in `calloc`, the `INT_MIN` overflow in `itoa`).

### What the library contains

| Part | Content | Functions |
| :--- | :--- | ---: |
| 1 — libc re-implementations | Character classification, memory and string primitives, conversion | 23 |
| 2 — additional functions | Allocation-backed strings, character/callback mapping, output to file descriptors | 11 |
| 3 — linked list | Node and list management API | 9 |
| | **Total** | **43** |

**Deliverables**

| Item | Path |
| :--- | :--- |
| Static library | `libft.a` (repository root) |
| Public header | `libft.h` (repository root) |
| Build script | `Makefile` (repository root) |
| Sources | `ft_*.c` (repository root) |

---

## Instructions

### Requirements

- A POSIX-like environment with `cc` (clang or gcc), `make` and `ar`.
- No third-party dependency, no libtool, no external runtime library.
- The whole project lives at the **root of the repository** — no `src/` or `include/` subdirectories.

### Build

```console
$ make
```

This compiles every `ft_*.c` with `-Wall -Wextra -Werror` (through `cc`) and archives the objects into `libft.a`.

Available rules:

| Rule | Effect |
| :--- | :--- |
| `make` / `make all` | Compile the sources and build `libft.a` |
| `make clean` | Remove object files |
| `make fclean` | Remove object files **and** `libft.a` |
| `make re` | `fclean` then `all` (full rebuild) |
| `make bonus` | Build the optional bonus library (see *Optional bonus part*) |

No unnecessary relinking: running `make` twice in a row does not rebuild anything, because `libft.a` depends on the object files and the object files depend on `libft.h`.

A quick sanity check after the build:

```console
$ ls -l libft.a
$ ar -t libft.a            # archive contents = one .o per source file
$ nm -g libft.a | grep ' T ft_' | wc -l   # should report every public symbol
```

### Using the library in another project

Link the archive and include the header:

```console
$ cc -Wall -Wextra -Werror -I ./libft ./main.c ./libft/libft.a -o my_program
```

Following the curriculum convention, when a later project is allowed to use `libft`, its sources and its `Makefile` are copied into a `libft/` folder inside that project, and the project's own `Makefile` builds `libft` through that `Makefile` **before** compiling the project itself.

### Testing

The subject does not require submitting tests, but comparing the `ft_` versions against the system ones is the only reliable way to know the edge cases were understood:

```console
$ cc -Wall -Wextra -Werror -D TEST main.c libft.a -o test && ./test
```

Practical notes:

- **Leaks**: build the test binary with `cc -fsanitize=address -g` or run it under `valgrind --leak-check=full`. Every `malloc` must have exactly one matching `free`; the list functions are the usual suspects.
- **Crashes**: a segmentation fault, bus error or double free on any reachable input makes the project non-functional, so NULL-ish and zero-length inputs are worth testing explicitly.
- **BSD-only functions**: `strlcpy`, `strlcat` and `bzero` are **not** part of glibc. To compare against the system implementation on a glibc machine, include `<bsd/string.h>` and link with `-lbsd` (`libbsd-dev`). This is a property of the host libc, not of the library.
- **Norm**: the code is checked with `norminette`. Any norm error in a submitted file (bonus included) invalidates the project.

### Optional bonus part

Bonuses are evaluated separately from the mandatory part and are not required. If they exist, they live in `*_bonus.{c,h}` files, are reachable through a `bonus` rule in the `Makefile`, and are subject to the same Norm, the same compiler flags and the same "no globals" rule. The mandatory build must still work on its own.

---

## Library reference (detailed description)

All functions are declared in `libft.h`, compiled with the required flags and use **no global variables**. Helpers that only exist to break a complex function down are declared `static`, so they stay private to their translation unit.

### Part 1 — libc re-implementations

Behaviour and prototypes follow the corresponding man pages exactly, except for the names (`ft_` prefix) and for the C99 `restrict` qualifier, which is deliberately **omitted** from the prototypes and never used as a compilation flag. None of these functions relies on an external function, apart from `calloc` and `strdup`, which are built on `malloc` as the subject requires.

| Function | Prototype | Behaviour |
| :--- | :--- | :--- |
| `ft_isalpha` | `int ft_isalpha(int c)` | 1 if `c` is a letter, else 0 |
| `ft_isdigit` | `int ft_isdigit(int c)` | 1 if `c` is a decimal digit, else 0 |
| `ft_isalnum` | `int ft_isalnum(int c)` | 1 if `c` is a letter or a digit, else 0 |
| `ft_isascii` | `int ft_isascii(int c)` | 1 if `c` is in the ASCII range (0–127), else 0 |
| `ft_isprint` | `int ft_isprint(int c)` | 1 if `c` is printable (space included), else 0 |
| `ft_strlen` | `size_t ft_strlen(const char *s)` | Length of `s`, terminator excluded (no allocation) |
| `ft_memset` | `void *ft_memset(void *s, int c, size_t n)` | Fills `n` bytes of `s` with `c`; returns `s` |
| `ft_bzero` | `void ft_bzero(void *s, size_t n)` | Sets `n` bytes of `s` to zero (no return value) |
| `ft_memcpy` | `void *ft_memcpy(void *dest, const void *src, size_t n)` | Copies `n` bytes; overlapping regions are undefined |
| `ft_memmove` | `void *ft_memmove(void *dest, const void *src, size_t n)` | Copies `n` bytes, safe when `dest` and `src` overlap |
| `ft_strlcpy` | `size_t ft_strlcpy(char *dst, const char *src, size_t size)` | NUL-terminated copy, at most `size - 1` bytes and nothing at all when `size` is 0; returns the length of `src` |
| `ft_strlcat` | `size_t ft_strlcat(char *dst, const char *src, size_t size)` | Appends `src` to `dst` within `size`; returns the total length it tried to create |
| `ft_toupper` | `int ft_toupper(int c)` | Lowercase letter → uppercase, other characters unchanged |
| `ft_tolower` | `int ft_tolower(int c)` | Uppercase letter → lowercase, other characters unchanged |
| `ft_strchr` | `char *ft_strchr(const char *s, int c)` | First occurrence of `c` in `s` (the terminator included); `NULL` if absent |
| `ft_strrchr` | `char *ft_strrchr(const char *s, int c)` | Last occurrence of `c` in `s`; `NULL` if absent |
| `ft_strncmp` | `int ft_strncmp(const char *s1, const char *s2, size_t n)` | Compares at most `n` bytes, as `unsigned char` |
| `ft_memchr` | `void *ft_memchr(const void *s, int c, size_t n)` | First occurrence of byte `c` in the first `n` bytes of `s` |
| `ft_memcmp` | `int ft_memcmp(const void *s1, const void *s2, size_t n)` | Byte-wise comparison of two memory areas |
| `ft_strnstr` | `char *ft_strnstr(const char *haystack, const char *needle, size_t len)` | Locates `needle` in `haystack`, not looking beyond `len`; an empty `needle` matches immediately |
| `ft_atoi` | `int ft_atoi(const char *nptr)` | Skips leading whitespace, honours an optional sign, then parses digits, as `(int)strtol(nptr, NULL, 10)` does; no error detection, no `errno` |
| `ft_calloc` | `void *ft_calloc(size_t nmemb, size_t size)` | `malloc` of `nmemb * size` bytes, zero-filled; `NULL` on failure |
| `ft_strdup` | `char *ft_strdup(const char *s)` | `malloc`-ed copy of `s`; `NULL` on failure |

**Three details the library commits to explicitly:**

1. The classification functions return exactly **1** on a match and **0** otherwise. This differs from glibc, where the man page only guarantees "a non-zero value" on a match.
2. `ft_calloc(0, x)` and `ft_calloc(x, 0)` return a **unique pointer that can be safely passed to `free()`**, as the subject requires — this is where host `calloc` implementations may legitimately disagree.
3. `ft_memcpy` with overlapping areas is *undefined behaviour* by definition and is therefore not "fixed"; `ft_memmove` is the function to use instead.

### Part 2 — additional functions

These functions either do not exist in libc or exist in a different shape. Everything that allocates returns `NULL` on allocation failure — a check the caller owes to itself. Except for `ft_split`, which allocates its array **and** every string in it, each function returning `char *` allocates a single block, and no function ever takes ownership of its arguments.

| Function | Prototype | Behaviour / allocation |
| :--- | :--- | :--- |
| `ft_substr` | `char *ft_substr(char const *s, unsigned int start, size_t len)` | Substring of `s` starting at `start`, at most `len` bytes; empty string if `start` is past the end. `malloc`. |
| `ft_strjoin` | `char *ft_strjoin(char const *s1, char const *s2)` | New string = `s1` followed by `s2`. `malloc`. |
| `ft_strtrim` | `char *ft_strtrim(char const *s1, char const *set)` | Copy of `s1` with the characters of `set` removed from both ends only. `malloc`. |
| `ft_split` | `char **ft_split(char const *s, char c)` | `NULL`-terminated array of independently allocated strings; the array itself is allocated too and contains no empty entries. Released by freeing each string, then the array. `malloc`, `free`. |
| `ft_itoa` | `char *ft_itoa(int n)` | Decimal representation of `n`, negative numbers included. `malloc`. |
| `ft_strmapi` | `char *ft_strmapi(char const *s, char (*f)(unsigned int, char))` | New string built by applying `f(index, character)` to each character; the source string is untouched. `malloc`. |
| `ft_striteri` | `void ft_striteri(char *s, void (*f)(unsigned int, char *))` | Applies `f(index, &character)` **in place**, so `f` may modify the string. No allocation. |
| `ft_putchar_fd` | `void ft_putchar_fd(char c, int fd)` | Writes `c` to `fd`. `write`. |
| `ft_putstr_fd` | `void ft_putstr_fd(char *s, int fd)` | Writes `s` to `fd`. `write`. |
| `ft_putendl_fd` | `void ft_putendl_fd(char *s, int fd)` | Writes `s` followed by a newline to `fd`. `write`. |
| `ft_putnbr_fd` | `void ft_putnbr_fd(int n, int fd)` | Writes the decimal representation of `n` to `fd`. `write`. |

`ft_putnbr_fd` handles `INT_MIN` without computing `-n` on the signed value, which is the classic overflow trap of this exercise; `ft_itoa` shares the same care.

### Part 3 — linked list

The node type is declared in `libft.h`:

```c
typedef struct s_list
{
    void    *content;
    struct s_list *next;
} t_list;
```

`content` is a `void *`, so a node can carry any payload; `next` is the address of the following node, or `NULL` for the last one. **The library never frees a payload it did not allocate**: the `del` callback handed in by the caller is the only thing allowed to release `content`.

| Function | Prototype | Behaviour / ownership |
| :--- | :--- | :--- |
| `ft_lstnew` | `t_list *ft_lstnew(void *content)` | New node with `content`, `next == NULL`. `malloc`. |
| `ft_lstadd_front` | `void ft_lstadd_front(t_list **lst, t_list *new)` | Inserts `new` at the head; works on an empty list (`*lst == NULL`). |
| `ft_lstsize` | `unsigned int ft_lstsize(t_list *lst)` | Number of nodes; an empty list is 0. |
| `ft_lstlast` | `t_list *ft_lstlast(t_list *lst)` | Last node, or `NULL` for an empty list. |
| `ft_lstadd_back` | `void ft_lstadd_back(t_list **lst, t_list *new)` | Appends `new`; sets the head directly when the list is empty. |
| `ft_lstdelone` | `void ft_lstdelone(t_list *lst, void (*del)(void *))` | Frees `content` through `del`, frees the node itself, and **nothing else** — successors stay alive. |
| `ft_lstclear` | `void ft_lstclear(t_list **lst, void (*del)(void *))` | Walks the list, freeing each node and its content, and finally sets `*lst` to `NULL`. |
| `ft_lstiter` | `void ft_lstiter(t_list *lst, void (*f)(void *))` | Calls `f(content)` on every node; the list structure is not modified. |
| `ft_lstmap` | `t_list *ft_lstmap(t_list *lst, void *(*f)(void *), void (*del)(void *))` | Builds a **new** list from `f(content)`; on allocation failure the partially built list is released with `del` and `NULL` is returned. |

---

## Technical choices and constraints

- **No global variables.** All state travels through parameters and return values; the only file-scope symbols are the `static` helpers.
- **`static` helpers.** Anything that is not part of the public API but is needed to keep a function readable is `static`, so it cannot collide with another project's symbols at link time.
- **Strict compilation.** `-Wall -Wextra -Werror`, `cc` as the compiler, no warning tolerated. `-std=c99` is not used, and the `restrict` qualifier is kept out of the prototypes.
- **`ar`, not libtool.** The archive is produced with `ar rcs libft.a *.o`; libtool is forbidden by the subject.
- **No unused files.** Every submitted `.c` file is referenced by the `Makefile` and provides a function that is part of the requested set.
- **Ownership rules.** Functions returning `char *`/`char **` allocate and return ownership to the caller; `ft_striteri` and the `ft_put*_fd` family allocate nothing; `del`-based list functions only free what they created themselves.
- **Failure is reported, not hidden.** An allocation failure yields `NULL`; no function aborts, exits, or prints an error — that policy belongs to the caller.
- **Portability.** The archive depends only on the C standard library (`malloc`, `free`) and POSIX `write(2)`, so it links unchanged on both Linux and macOS.

## Project structure

```text
.
├── Makefile
├── libft.h
├── ft_isalpha.c
├── ft_isdigit.c
├── ft_isalnum.c
├── ft_isascii.c
├── ft_isprint.c
├── ft_strlen.c
├── ft_memset.c
├── ft_bzero.c
├── ft_memcpy.c
├── ft_memmove.c
├── ft_strlcpy.c
├── ft_strlcat.c
├── ft_toupper.c
├── ft_tolower.c
├── ft_strchr.c
├── ft_strrchr.c
├── ft_strncmp.c
├── ft_memchr.c
├── ft_memcmp.c
├── ft_strnstr.c
├── ft_atoi.c
├── ft_calloc.c
├── ft_strdup.c
├── ft_substr.c
├── ft_strjoin.c
├── ft_strtrim.c
├── ft_split.c
├── ft_itoa.c
├── ft_strmapi.c
├── ft_striteri.c
├── ft_putchar_fd.c
├── ft_putstr_fd.c
├── ft_putendl_fd.c
├── ft_putnbr_fd.c
├── ft_lstnew.c
├── ft_lstadd_front.c
├── ft_lstsize.c
├── ft_lstlast.c
├── ft_lstadd_back.c
├── ft_lstdelone.c
├── ft_lstclear.c
├── ft_lstiter.c
├── ft_lstmap.c
├── ft_*_bonus.c        (optional)
└── libft_bonus.h       (optional)
```

---

## Resources

### Classic references

- **Man pages** — the authoritative source for every Part 1 function: `man 3 strlen`, `man 3 memmove`, `man 3 strlcpy`, `man 3 calloc`, … Read the `BUGS`, `RETURN VALUE` and `NOTES` sections, not only the synopsis.
- **POSIX / Single UNIX Specification** — [pubs.opengroup.org](https://pubs.opengroup.org/onlinepubs/9699919799/) — specification-level behaviour of the string, memory and character functions.
- **OpenBSD `strlcpy`/`strlcat`** — the functions originate there, and the original paper explains *why* they were designed as truncating, size-returning copies.
- **ISO/IEC 9899 (C standard)** — in particular §7.24 (string handling), §7.22 (general utilities, `malloc`/`calloc`) and the `restrict` qualifier in §6.7.3.
- **cppreference.com** — [en.cppreference.com/w/c/string/byte](https://en.cppreference.com/w/c/string/byte) — quick lookup of prototypes and edge cases.
- **The Norm** (42 Norm, latest version on the intranet) — the formatting, naming and function-length rules the whole project must satisfy.
- **cppreference `ar` / `nm` docs and `man 1 ar`** — how a static archive is actually created and inspected.
- **"The C Programming Language"**, B. Kernighan & D. Ritchie — the canonical description of pointers, arrays and the string representation used here.
- **`norminette`** — [github.com/42School/norminette](https://github.com/42School/norminette) — the checker used before every submission.
- **`libbsd`** — [libbsd project](https://libbsd.freedesktop.org/) — provides `strlcpy`, `strlcat` and `bzero` on glibc systems for comparison tests.
- **Valgrind / AddressSanitizer documentation** — the standard way to prove that the allocation-backed functions and the list API do not leak.
- **42 intranet: the AI FAQ** — the curriculum's stance on AI as a learning tool, referenced by the subject's AI instructions.

### How AI was used in this project

*This section is part of the submission and must describe the actual use of AI tools; adjust it if the real share of work differed.*

| Area | Was AI used? | For what exactly |
| :--- | :--- | :--- |
| Function implementations (`ft_*.c`) | No | All 43 functions were written, debugged and normed by hand. The logic — the `memmove` direction decision, the `strlcat` return value, the `ft_split` free path, the `INT_MIN` handling in `ft_itoa` — is the author's own reasoning. |
| Reading the man pages / the subject | Partly | AI was used to rephrase a man-page paragraph when the wording was unclear, and to list the edge cases worth testing for a given function. Prototypes and behaviour were always confirmed against `man 3` and the subject itself, never taken from the model. |
| Debugging | Partly | When a test failed, AI was asked *why* a construct behaves the way it does (e.g. why `strncat`-style code loses the terminator, or why a `free` inside a loop double-frees). The corrected code was reasoned through and rewritten by the author; no fix was pasted in blindly. |
| Test programs | Yes | AI helped generate the comparison harness that calls both the `ft_` function and the libc version on the same inputs and diffs the results, including zero-length and `NULL`-ish cases. These tests are not part of the submission. |
| Norm compliance | Partly | AI was consulted on Norm rules that were misinterpreted (line length vs. tab width, the function-count-per-file rule). `norminette` remained the judge. |
| Makefile | Partly | The dependency graph was discussed with AI; the final `Makefile` was typed, read and understood line by line. |
| This README | Yes | The document was drafted with AI assistance and then reviewed and corrected by the author, in line with the description of the library above. |

**What was not delegated:** understanding the behaviour of the functions, choosing the data structures, deciding the error-handling policy, and explaining any line of code during the peer evaluation. Those are the parts the curriculum actually evaluates, and a model cannot defend them on the author's behalf. No AI was used to produce the code of the mandatory part, and no AI tool was used as a substitute for reading the documentation.

---

## Evaluation notes

During the peer evaluation the library is compiled from scratch, the `Makefile` rules are exercised (`all`, `clean`, `fclean`, `re`), the `ft_` functions are compared against their libc counterparts on normal and hostile inputs, and the list functions are tested for leaks. A small live modification may be requested (a behaviour tweak, a few rewritten lines, or a small additional feature) to confirm that the code is understood rather than copied — the sources are therefore expected to be readable, documented and fully owned by their author.
