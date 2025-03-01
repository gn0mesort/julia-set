# Julia Set Renderer

This is a program using [SDL2](https://www.libsdl.org/) and [OpenGL](https://www.opengl.org/) 4.5 that renders an
animation of a number of [julia sets](https://en.wikipedia.org/wiki/Julia_set) on a compatible GPU. These sets are
of the form: <code>z<sup>2</sup> + 0.7885<em>e</em><sup>A * <em>i</em></sup></code>

## Dependencies

To compile this program you will need the following:

- A standard C++20 compiler and run-time environment
- An implementation of the [Meson](https://mesonbuild.com/) build system and a compatible backend (e.g.,
  [Ninja](https://ninja-build.org/))
- A copy of the SDL2 library and development header files

To run the program you need:

- A standard C++20 run-time environment
- A copy of the SDL2 library
- A working implementation of OpenGL 4.5 (or higher)

## Building

### Preparing the Build Environment

For ease of use, I've provided both Meson and the Ninja build backend as Python requirements. To install them this way
you should first prepare a virtual environment as follows:

```sh
# Prepare a Python virtual environment in the directory .venv
python3 -m venv .venv
```

Next, you'll need to activate the virtual environment (so that you don't install system-wide). The activation method
varies depending on your system and shell. For Bash run the following:

```sh
# Activate the virtual environment in the .venv directory
source .venv/bin/activate
```

At this point, you can install the build system by running:

```sh
python3 -m pip install -r requirements.txt
```

### Configuring the Build System

With the build environment prepared, the next step is to configure the Meson build system. To do this, you need to
setup a build directory by running:

```sh
# Setup a new build directory named "build"
meson setup build
```

Next, you can configure your build. Despite being a fairly simple program there are a couple of project specific
options. These are the following:

| Option | Description | Default | Example |
| --- | --- | --- | --- |
| colors | A feature that controls whether or not the renderer will display a color image. | `enabled` | `meson configure build -Dcolors=disabled` |
| window_width | The initial width of the output window in pixels. | 1920 pixels | `meson configure build -Dwindow_width=640` |
| window_height | The initial height of the output window in pixels. | 1080 pixels | `meson configure build -Dwindow_height=360` |

### Compiling

When everything is configured to your liking you can compile the usual way:

```sh
# Compile the targets described in the "build" directory.
meson compile -C build
```

### Installing

I don't think this program is really interesting enough to install, but you can still do so. As usual you can
install with:

```sh
# Install all the files described by the configuration located in "build".
# You can add --dry-run to determine what would be installed without actually performing the installation.
meson install -C build
```

## Controls

When running the application you can use the W, A, S, and D keys or the arrow keys to pan the scene in two
dimensions. You can also use your mouses scroll wheel to zoom in or out of the scene. This makes finer details of the
fractals much easier to observe. If you want pause the animation at any point, you can press P.

## Acknowledgements

To properly load OpenGL 4.5, I'm using source code generated by [Glad](https://github.com/Dav1dde/glad). The generated
source code ([`include/glad/glad.h`](/include/glad/glad.h) and [`src/glad/glad.c`](/src/glad/glad.c)) are public
domain.

The Glad generator also provides a copy of `khrplatform.h` found at
[`include/KHR/khrplatform.h`](/include/KHR/khrplatform.h). This file is licensed as follows:

> Copyright (c) 2008-2018 The Khronos Group Inc.
>
> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and/or associated
> documentation files (the "Materials"), to deal in the Materials without restriction, including without limitation
> the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Materials, and to
> permit persons to whom the Materials are furnished to do so, subject to the following conditions:
>
> The above copyright notice and this permission notice shall be included in all copies or substantial portions of the
> Materials.
>
> THE MATERIALS ARE PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO
> THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
> AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
> TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE MATERIALS OR THE USE OR OTHER DEALINGS IN THE
> MATERIALS.

## Licensing

Copyright (C) 2024 Alexander Rothman <[gnomesort@megate.ch](mailto:gnomesort@megate.ch)>

This program is free software: you can redistribute it and/or modify it under the terms of the GNU Affero General
Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any
later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied
warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU Affero General Public License for more
details.

You should have received a copy of the GNU Affero General Public License along with this program. If not, see
<[https://www.gnu.org/licenses/](https://www.gnu.org/licenses/)>.
