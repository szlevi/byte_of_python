# Standard Library #

The Python Standard Library contains a huge number of useful modules
and is part of every standard Python installation. It is important to
become familiar with the Python Standard Library since many problems
can be solved quickly if you are familiar with the range of things
that these libraries can do.

We will explore some of the commonly used modules in this library. You
can find complete details for all of the modules in the Python
Standard Library in the
['Library Reference' section](http://docs.python.org/3/library/) of
the documentation that comes with your Python installation.

Let us explore a few useful modules.

Note

:   If you find the topics in this chapter too advanced, you may skip
    this chapter. However, I highly recommend coming back to this
    chapter when you are more comfortable with programming using
    Python.

## sys module ##

The `sys` module contains system-specific functionality. We have
already seen that the `sys.argv` list contains the command-line
arguments.

Suppose we want to check the version of the Python command being used
so that, say, we want to ensure that we are using at least
version 3. The `sys` module gives us such functionality.

~~~
$ python3
>>> import sys
>>> sys.version_info
sys.version_info(major=3, minor=3, micro=2, releaselevel='final', serial=0)
>>> sys.version_info.major >= 3
True
~~~

How It Works:

The `sys` module has a `version_info` tuple that gives us the version
information. The first entry is the major version. We can check this
to, for example, ensure the program runs only under Python 3.0:

Save as `versioncheck.py`:

~~~python
import sys, warnings
if sys.version_info.major < 3:
    warnings.warn("Need Python 3.0 for this program to run",
        RuntimeWarning)
else:
    print('Proceed as normal')
~~~

Output:

~~~
$ python2.7 versioncheck.py
versioncheck.py:6: RuntimeWarning: Need Python 3.0 for this program to run
  RuntimeWarning)

$ python3 versioncheck.py
Proceed as normal
~~~

How It Works:

We use another module from the standard library called `warnings` that
is used to display warnings to the end-user. If the Python version
number is not at least 3, we display a corresponding warning.

## logging module ##

What if you wanted to have some debugging messages or important
messages to be stored somewhere so that you can check whether your
program has been running as you would expect it? How do you "store
somewhere" these messages? This can be achieved using the `logging`
module.

Save as `use_logging.py`:

~~~python
import os, platform, logging

if platform.platform().startswith('Windows'):
    logging_file = os.path.join(os.getenv('HOMEDRIVE'), os.getenv('HOMEPATH'), 'test.log')
else:
    logging_file = os.path.join(os.getenv('HOME'), 'test.log')

print("Logging to", logging_file)

logging.basicConfig(
    level=logging.DEBUG,
    format='%(asctime)s : %(levelname)s : %(message)s',
    filename = logging_file,
    filemode = 'w',
)

logging.debug("Start of the program")
logging.info("Doing something")
logging.warning("Dying now")
~~~

Output:

~~~
$ python3 use_logging.py
Logging to C:\Users\swaroop\test.log
~~~

If we check the contents of `test.log`, it will look something like
this:

~~~
2012-10-26 16:52:41,339 : DEBUG : Start of the program
2012-10-26 16:52:41,339 : INFO : Doing something
2012-10-26 16:52:41,339 : WARNING : Dying now
~~~

How It Works:

We use three modules from the standard library - the `os` module for
interacting with the operating system, the `platform` module for
information about the platform i.e. the operating system and the
`logging` module to *log* information.

First, we check which operating system we are using by checking the
string returned by `platform.platform()` (for more information, see
`import platform; help(platform)`). If it is Windows, we figure out
the home drive, the home folder and the filename where we want to
store the information. Putting these three parts together, we get the
full location of the file. For other platforms, we need to know just
the home folder of the user and we get the full location of the file.

We use the `os.path.join()` function to put these three parts of the
location together. The reason to use a special function rather than
just adding the strings together is because this function will ensure
the full location matches the format expected by the operating system.

We configure the `logging` module to write all the messages in a
particular format to the file we have specified.

Finally, we can put messages that are either meant for debugging,
information, warning or even critical messages. Once the program has
run, we can check this file and we will know what happened in the
program, even though no information was displayed to the user running
the program.

## Module of the Week Series ##

There is much more to be explored in the standard library such as
[debugging](http://docs.python.org/3/library/pdb.html),
[handling command line options](http://docs.python.org/3/library/argparse.html),
[regular expressions](http://docs.python.org/3/library/re.html) and so
on.

The best way to further explore the standard library is to read Doug
Hellmann's excellent
[Python Module of the Week](http://pymotw.com/2/contents.html) series
(also available as a
[book](http://doughellmann.com/python-standard-library-by-example))
and reading the [Python documentation](http://docs.python.org/3/).

## Summary ##

We have explored some of the functionality of many modules in the
Python Standard Library. It is highly recommended to browse through
the
[Python Standard Library documentation](http://docs.python.org/3/library/)
to get an idea of all the modules that are available.

Next, we will cover various aspects of Python that will make our tour
of Python more *complete*.
