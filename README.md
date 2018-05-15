# Clip Library
*Copyright (C) 2015-2018 David Capello*

> Distributed under [MIT license](LICENSE.txt)

Library to copy/retrieve content to/from the clipboard/pasteboard.

## Features

Available features on Windows, macOS, and Linux (X11):

* Copy/paste UTF-8 text.
* Copy/paste user-defined data.
* Copy/paste RGB/RGBA images. This library use non-premultiplied alpha RGB values.

## Example

```cpp
#include "clip.h"
#include <iostream>

int main() {
  clip::set_text("Hello World");

  std::string value;
  clip::get_text(value);
  std::cout << value << "\n";
}
```

## User-defined clipboard formats

```cpp
#include "clip.h"

int main() {
  clip::format my_format =
    clip::register_format("com.appname.FormatName");

  int value = 32;

  clip::lock l;
  l.clear();
  l.set_data(clip::text_format(), "Alternative text for value 32");
  l.set_data(my_format, &value, sizeof(int));
}
```

* [Limited number of clipboard formats on Windows](http://blogs.msdn.com/b/oldnewthing/archive/2015/03/19/10601208.aspx)

## To-do

* Linux/X11: Keep clipboard content alive even when the process is closed
* Linux/X11: Use `INCR` property to [transfer large data](https://www.x.org/releases/X11R7.6/doc/xorg-docs/specs/ICCCM/icccm.html#large_data_transfers)

## Who is using this library?

`clip` is being used in the following applications:

* [Aseprite](https://github.com/aseprite/aseprite)
