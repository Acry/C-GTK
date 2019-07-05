

# Building GTK Programs using Meson/Ninja


## Requirements
The Meson Example has two main dependencies.

Python 3 and Ninja

Ninja is needed if you use the Ninja backend. But Meson can also generate native VS and XCode project files.


## Plain C Example

### C-Source

Create a file main.c which holds the source.

```C
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char **argv)
{
  printf("Hello World!\n");
  return EXIT_SUCCESS;
}
```

### Meson build description

Then create a Meson build description and put it in a file called meson.build in the same directory.

Containing the following lines.

```mono
project('tutorial', 'c')
executable('demo', 'main.c')
```

You are now ready to build.

### Build-Process

#### Initialization

Create the directory for building.

Issue:

`meson builddir`

To create a build directory to hold all of the compiler output.

**Meson does not permit in-source builds.**

Common convention is to put the default build directory in a subdirectory of your top level source directory.

When Meson is running it prints the following output.

```mono
The Meson build system
Version: 0.51.0
Source dir: /home/carsten/nas/IT/MyProjects/C-GTK/Building
Build dir: /home/carsten/nas/IT/MyProjects/C-GTK/Building/builddir
Build type: native build
Project name: tutorial
Project version: undefined
C compiler for the build machine: ccache cc (gcc 9.1.0 "cc (GCC) 9.1.0")
C compiler for the host machine: ccache cc (gcc 9.1.0 "cc (GCC) 9.1.0")
Build machine cpu family: x86_64
Build machine cpu: x86_64
Build targets in project: 1
Found ninja-1.9.0 at /usr/bin/ninja
```

#### Building

`cd builddir`

`ninja`
```mono
[2/2] Linking target demo.
```

Now the binary should be there and it can be executed.

`./demo`


## GTK Example

main.c

```C
#include <gtk/gtk.h>

int main(int argc, char **argv)
{
  GtkWidget *win;
  gtk_init(&argc, &argv);
  win = gtk_window_new(GTK_WINDOW_TOPLEVEL);
  gtk_window_set_title(GTK_WINDOW(win), "Hello there");
  g_signal_connect(win, "destroy", G_CALLBACK(gtk_main_quit), NULL);
  gtk_widget_show(win);
  gtk_main();
}
```

Create the Meson file, instructing it to find and use the GTK+ libraries.

meson.build
```mono
project('tutorial', 'c')
gtkdep = dependency('gtk+-3.0')
executable('demo', 'main.c', dependencies : gtkdep)
```

`meson builddir`

```mono
The Meson build system
Version: 0.51.0
Source dir: /home/carsten/nas/IT/MyProjects/C-GTK/Building/Meson/GTK Example
Build dir: /home/carsten/nas/IT/MyProjects/C-GTK/Building/Meson/GTK Example/builddir
Build type: native build
Project name: tutorial
Project version: undefined
C compiler for the build machine: ccache cc (gcc 9.1.0 "cc (GCC) 9.1.0")
C compiler for the host machine: ccache cc (gcc 9.1.0 "cc (GCC) 9.1.0")
Build machine cpu family: x86_64
Build machine cpu: x86_64
Found pkg-config: /usr/bin/pkg-config (1.6.1)
Run-time dependency gtk+-3.0 found: YES 3.24.9
Build targets in project: 1
Found ninja-1.9.0 at /usr/bin/ninja
```

`cd builddir`

`ninja`

`./demo`

## Cleaning

### Meson

> Secondly this makes it very easy to clean your projects: just delete the build subdirectory and you are done. There is no need to guess whether you need to run make clean, make distclean, make mrproper or something else. When you delete a build subdirectory there is no possible way to have any lingering state from your old builds.

### Ninja clean

clean

remove built files. By default it removes all built files except for those created by the generator. Adding the -g flag also removes built files created by the generator (see the rule reference for the generator attribute). Additional arguments are targets, which removes the given targets and recursively all files built for them.

If used like:

`ninja -t clean -r rules`

it removes all files built using the given rules.

Files created but not referenced in the graph are not removed. This tool takes in account the -v and the -n options (note that -n implies -v).


## Links

<https://mesonbuild.com/>
<https://mesonbuild.com/Tutorial.html>

<https://ninja-build.org/>

<https://en.wikipedia.org/wiki/Meson_(software)>

<https://www.rojtberg.net/1481/do-not-use-meson/>


