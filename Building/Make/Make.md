

# Building GTK Programs using GNU-Make


GNU-Make is part of the GNU-OS.

## Using Package Config

Visit [POSIX-Shell](../POSIX-Shell/Shell.md)

CFLAGS are Compiler Flags
LDFLAGS are Linker Flags

Targets are files to build.
Recipes are needed to build targets.
Phony Targets doesn't address a file.


## Colored output with tput

tput is part of ncurses.

Define the Function:

```Make
define colorecho
      @tput setaf 2
      @echo $1
      @tput sgr0
endef
```

Call the function:

```Make
$(call colorecho,"$@ success. ./\"$@\" to execute.")
```

Use `make -f Makefile_tput` to check the Makefile.


## Building

`make -B` - build over, ignore timestamps
`make -f` - use distinct Makefile
`make -k` - keepgoing, even with errors

`make all` - all targets

## Cleaning
`make clean`

