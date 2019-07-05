CC ?= gcc
# ?= The Variable is only set if if undefined.

# PKGCONFIG = $(shell which pkg-config)

CFLAGS   = -no-pie -Wall -Wextra -mtune=native `pkg-config --cflags gtk+-3.0`
LDFLAGS  = `pkg-config --libs gtk+-3.0`

# Using backticks is deprecated, but often seen.
# $(pkg-config --cflags gtk+-3.0) is the correct syntax.

TARGETS = demo

.PHONY: all
all: $(TARGETS)

demo:   main.c
	@$(CC) $(CFLAGS) -o $@ $< $(LDFLAGS)
	./demo &

.PHONY: clean
clean:
	@rm $(TARGETS) 2>/dev/null || true

# @	Supresses the output

# $<	First Dependency
# $@	Target Name
# $+	List of all Dependencies
# $^	Unique list of all Dependencies

