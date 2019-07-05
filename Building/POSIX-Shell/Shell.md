

# Building GTK Programs using a POSIX-Shell


```shell
cc -no-pie -o demo main.c $(pkg-config --cflags --libs gtk+-3.0)
```

You can paste that line to your Shell or put it in a file like I did.
Either you turn the executeable flag on with with `chmod +x` or you invoke the file with your shell `sh compile.sh`.


cc should be a symbolic link to your compiler.

I am using gcc version 9.1.0 and it was configured with:

`--enable-default-pie`, so I need to pass `-no-pie` to build a default executable.

default pie (position indepentend code):

$ file demo
demo: ELF 64-bit LSB pie executable

`-no-pie` argument:

$ file demo
demo: ELF 64-bit LSB executable

If you want to see what pkg-config adds to the arguments, just pass `pkg-config --cflags --libs gtk+-3.0` to your shell.

```shell
$ pkg-config --cflags --libs gtk+-3.0
-I/usr/include/gtk-3.0 -I/usr/include/pango-1.0 -I/usr/include/glib-2.0 -I/usr/lib/glib-2.0/include -I/usr/lib/libffi-3.2.1/include -I/usr/include/fribidi -I/usr/include/harfbuzz -I/usr/include/freetype2 -I/usr/include/libpng16 -I/usr/include/uuid -I/usr/include/cairo -I/usr/include/pixman-1 -I/usr/include/gdk-pixbuf-2.0 -I/usr/include/libmount -I/usr/include/blkid -I/usr/include/gio-unix-2.0 -I/usr/include/libdrm -I/usr/include/atk-1.0 -I/usr/include/at-spi2-atk/2.0 -I/usr/include/at-spi-2.0 -I/usr/include/dbus-1.0 -I/usr/lib/dbus-1.0/include -pthread -lgtk-3 -lgdk-3 -lz -lpangocairo-1.0 -lpango-1.0 -latk-1.0 -lcairo-gobject -lcairo -lgdk_pixbuf-2.0 -lgio-2.0 -lgobject-2.0 -lglib-2.0 
```

