Handy guide to virtualenv
=========================

This guide will explain a way to get one or more Python packages running from
a single directory, separated from the rest of your computer.

The steps are:

  1. Get `python`.
  2. Get `virtualenv`.
  3. Use `virtualenv` to create a directory including `pip`.
  4. Use `pip` to upgrade itself.
  5. Use `pip` to install the packages, and any other packages they need.

This approach results in a "virtualenv directory" containing the packages,
together with a `python` command that can import and run them.

The steps are explained in more detail in the sections below.


Alternative guides
------------------

The official [virtualenv documentation][g1] is a bit easier to read than this,
so you might prefer to read that first.

[g1]: https://virtualenv.pypa.io/en/latest/installation.html

There's a very short guide in [this Stack Overflow answer][g2].

[g2]: http://stackoverflow.com/a/5177027


Quick start
-----------

On some platforms `python` and `virtualenv` are already installed (the first
two steps), and the remaining three steps can be completed by running:

    virtualenv ENV
    ENV/bin/pip install -U pip        # Use "ENV/Scripts/pip" on Windows.
    ENV/bin/pip install -U PACKAGE

where _ENV_ is a name for the virtualenv directory to create, and
_PACKAGE_ is the name of the package to install.

You can choose whatever name you like for the virtualenv directory.  This
guide will keep calling it `ENV`.


If this works for you, you can stop reading now.  Otherwise, read on as we
cover each step in more depth.


Get `python`
------------

You may already have Python installed, or you may be able to install it from your system's package manager.

Run `python --version`.  If it prints a suitable version, you can skip this
step.  If not, some systems will suggest further steps at this point.
See the documentation of the packages you are trying to install to find out
what counts as a suitable version.

Otherwise, download and install Python from https://www.python.org.  Add it to
your PATH, which is an option in the installer in recent versions of Python.


Get `virtualenv`
----------------

You may already have virtualenv installed, or you may be able to install it
from your system's package manager.

Run `virtualenv --version`.  If it prints a suitable version, you can skip
this step.  If not, some systems will suggest further steps at this point.
A suitable version usually means a recent one, but you may be happy to settle
for anything that works.

Otherwise, download and unzip the latest virtualenv zip file from
[here](https://github.com/pypa/virtualenv/releases) (which also tells you
which versions are recent).  Use `python UNZIPPED/virtualenv.py` as
`virtualenv` in the rest of this guide, where _UNZIPPED_ is the unzipped
directory.

One way to unzip the downloaded virtualenv zip file (_ZIPFILE_) is to use:

    python -m zipfile -e ZIPFILE .

That only works with a recent version of Python, but you probably know how to
unzip files anyway.

See https://virtualenv.pypa.io/en/latest/installation.html if you need further
help on installing `virtualenv` itself.


Use `virtualenv` to create a directory including `pip`
------------------------------------------------------

Run:

    virtualenv ENV

where _ENV_ is the directory to create.  You may use something other than
`virtualenv`, as suggested in the previous step.


Use `pip` to upgrade itself
---------------------------

Run:

    ENV/bin/pip install -U pip

where _ENV_ is the virtualenv directory, and `bin` should be `Scripts` on
Windows.


Use `pip` to install the packages, and any other packages they need
-------------------------------------------------------------------

Run:

    ENV/bin/pip install -U PACKAGE

or:

    ENV/bin/pip install -U -r requirements.txt

where _ENV_ is the virtualenv directory, _PACKAGE_ is the package name,
and `bin` should be `Scripts` on Windows.

`requirements.txt` is a list of the packages to install, one per line.

Each package name may be immediately followed (without a space) by a version
specifier such as `==1.2.0` or `>=1.2.0`.  The other details of what can be
put in these files are explained [here][1].

[1]: https://pip.readthedocs.org/en/stable/user_guide/#requirements-files

If your package fails to install, try updating the `setuptools` and `wheel`
packages and then try again:

    ENV/bin/pip install -U setuptools
    ENV/bin/pip install -U wheel

Otherwise, the most common cause of problems is that the package depends on
a working C compiler with the right header files available to it.  This
usually involves installing the right system packages, for instance with
`apt-get install SYSPACKAGE` on Debian/Ubuntu Linux.  Unfortunately, guessing
what _SYSPACKAGE_ should be often involves searching the web for the error
message you're getting.

You can find out what Python package versions have been installed in your
virtualenv directory by running:

    ENV/bin/pip freeze


Conclusion
----------

All being well, you now have a working "virtualenv directory", and can create
more of them as you need them.

You can test it by running:

    ENV/bin/python       # Use "ENV/Scripts/python" on Windows.

You should then be able to import the modules from the packages you installed
by typing:

```#python
    import MODULE
```

where _MODULE_ is an appropriate module name.  (Type `quit()` to exit Python).

You can also run any of the commands in the `bin` or `Scripts` directory, and
they will be able to use the installed packages.

Perhaps you'd like to read the [second part of this guide][PART-2], which
fills in a few more details?

Please raise issues if you have any questions, or if you have ideas for how to
improve this guide.

[PART-2]: virtualenv-guide-part-2.md
