Bloomberg Python API version 3.5+
================================

This directory contains an interface for interacting with Bloomberg API
services using the Python programming language.


Dependencies
------------

This SDK requires the following products:

- CPython version 3.4+

- Bloomberg C++ SDK version 3.5 or later

- Visual C++ 2010 (Windows) or GCC 4.1+ (Linux)


Installation
------------

Note that installation requires a working C compiler and the C headers
distributed as part of the Bloomberg C++ SDK.

1. Set the `BLPAPI_ROOT` environment variable to the location at which the
   Bloomberg C++ SDK is installed. (On Windows, this location may be of the
   form `C:\blp\API\APIv3\C++API\v3.5.2.1\`.)

2. To compile and install the `blpapi` Python package for all users, run

       > python setup.py install

   To compile and install the `blpapi` Python package for only the current
   user, run

       > python setup.py install --user

   (Note that the former command requires root/administrator access, while the
   latter does not.)

   Documentation on additional build and installation options is available by
   running

       > python setup.py --help

3. (optional) Copy the C++ SDK shared library/DLL to a standard library
   location (e.g. `/usr/lib` on Linux), or update the system-wide library path
   (configured by `/etc/ld.so.conf` on Linux and by setting the `PATH`
   environment variable on Windows) to include the directory containing the
   C++ SDK library.  Note that this step is not necessary for users who already
   have a system-wide installation of the C++ SDK, including Windows users who
   have the Bloomberg Terminal software installed.


Writing Bloomberg API Programs in Python
----------------------------------------

In order for python scripts to call Bloomberg API functions, the libraries
distributed as part of the Bloomberg C++ SDK must be available to the Python
interpreter.  Step 3 of installation, above, provides system-wide installation
of this library. Linux/Solaris/*nix users without system-wide installations
must set the `LD_LIBRARY_PATH` (or `DYLD_LIBRARY_PATH` on Darwin/MacOS X)
environment variable to include the directory containing the `blpapi3` shared
libraries.  Windows users may need to set the `PATH` variable to the
directory containing `blpapi3_32.dll` or `blpapi3_64.dll`. (Note that Windows
users with the Bloomberg Terminal software installed already have versions of
these libraries in their `PATH`.)

After installation, the `blpapi` module can be imported by a Python script or
within the CPython interpreter:

    >>> import blpapi
    >>> options = blpapi.SessionOptions()
    >>> options.setServerHost('localhost')
    >>> options.setServerPort(8194)
    >>> session = blpapi.Session(options)
    >>> session.start()

Note that many Python installations add the current directory to the module
search path. If the Python interpreter is invoked from the installer directory,
such a configuration will attempt to use the (incomplete) local `blpapi`
directory as a module. If the above `import` line fails with the message
`Import Error: No module named _internals`, move to a different directory
before invoking `python`.

Documentation for individual Bloomberg API classes and functions is provided
through Python's built-in help system.

Further documentation on programming the Bloomberg API is available in the
Developer's Guide, available at <http://open.bloomberg.com>.


Examples
--------

A collection of complete Python programs covering a wide range of typical API
usage is available in the `examples` directory, located in the same directory
as this `README` file. Note that many examples make use of command-line
arguments to specify server and authentication configuration; in most cases
usage information can be obtained by passing the `--help` option on the command
line.


Implementation Notes
--------------------

- The Python Bloomberg SDK does not provide direct support for Python `unicode`
  objects. Clients can pass unicode data to SDK functions accepting strings by
  calling `u.encode('utf-8')` for an appropriate `unicode` object `u`; a string
  `s` received from an SDK function can be converted to a `unicode` object by
  calling `s.decode('utf-8')`.

- Python Bloomberg SDK types do not provide support for the Python `copy` or
  `pickle` modules.


Copyright and License
---------------------

All files Copyright 2012 Bloomberg Finance L.P.

Permission is hereby granted, free of charge, to any person obtaining a copy of
this proprietary software and associated documentation files (the "Software"),
to use, publish, or distribute copies of the Software, and to permit persons to
whom the Software is furnished to do so.

Any other use, including modifying, adapting, reverse engineering, decompiling,
or disassembling, is not permitted.

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

