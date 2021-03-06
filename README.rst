+++++++++++++
Fault handler
+++++++++++++

.. image:: https://img.shields.io/pypi/v/faulthandler.svg
   :alt: Latest release on the Python Cheeseshop (PyPI)
   :target: https://pypi.python.org/pypi/faulthandler

.. image:: https://travis-ci.org/vstinner/faulthandler.svg?branch=master
   :alt: Build status of faulthandler on Travis CI
   :target: https://travis-ci.org/vstinner/faulthandler

.. image:: http://unmaintained.tech/badge.svg
   :target: http://unmaintained.tech/
   :alt: No Maintenance Intended

Fault handler for SIGSEGV, SIGFPE, SIGABRT, SIGBUS and SIGILL signals: display
the Python traceback and restore the previous handler. Allocate an alternate
stack for this handler, if sigaltstack() is available, to be able to allocate
memory on the stack, even on stack overflow (not available on Windows).

Import the module and call faulthandler.enable() to enable the fault handler.

Alternatively you can set the PYTHONFAULTHANDLER environment variable to a
non-empty value.

The fault handler is called on catastrophic cases and so it can only use
signal-safe functions (eg. it doesn't allocate memory on the heap). That's why
the traceback is limited: it only supports ASCII encoding (use the
backslashreplace error handler for non-ASCII characters) and limits each string
to 100 characters, doesn't print the source code in the traceback (only the
filename, the function name and the line number), is limited to 100 frames and
100 threads.

By default, the Python traceback is written to the standard error stream. Start
your graphical applications in a terminal and run your server in foreground to
see the traceback, or pass a file to faulthandler.enable().

faulthandler is implemented in C using signal handlers to be able to dump a
traceback on a crash or when Python is blocked (eg. deadlock).

This module is the backport for CPython 2.7. faulthandler is part of CPython
standard library since CPython 3.3: `faulthandler
<http://docs.python.org/dev/library/faulthandler.html>`_. For PyPy,
faulthandler is builtin since PyPy 5.5: use ``pypy -X faulthandler``.

Website:
https://faulthandler.readthedocs.io/

faulthandler 3.2 is the last version released by Victor Stinner. I maintained
it for 10 years in my free time for the great pleasure of Python 2 users, but
Python 2 is no longer supported upstream since 2020-01-01. Each faulthandler
release requires me to start my Windows VM, install Python 2.7 in 32-bit and
64-bit, install an old C compiler just for Python 2.7, and type manually some
commands to upload Windows binaries. Moreover, I have to fix some issues on
Travis CI and many small boring tasks. The maintenance is far from being free.
In 10 years, I got zero "thank you" (and 0€), only bug reports :-)
