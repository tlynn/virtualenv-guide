Handy guide to virtualenv
=========================

This guide will explain a way to get one or more Python packages running from
a single directory, separated from the rest of your computer.

The steps are:

  1. Get `python`.
  2. Get `virtualenv`.
  3. Use `virtualenv` to create a directory including `pip`.
  4. Use `pip` to install the packages, and any other packages they need.

This approach results in a "virtualenv directory" containing the packages,
together with a `python` command that can import and run them.

The steps are explained in more detail in the sections below.


Alternative guides
------------------

The official [virtualenv documentation][DOCS] is quite readable.

[DOCS]: https://virtualenv.readthedocs.org/en/latest/installation.html


Get `python`
------------

Install the latest version of Python, either via your system's package manager
or by downloading and running an installer from https://www.python.org/.


Get `virtualenv`
----------------

Download the latest [virtualenv zipapp file][ZIPAPP].

[ZIPAPP]: https://bootstrap.pypa.io/virtualenv.pyz

In place of `virtualenv` below, use:

    python <DOWNLOADS>/virtualenv.pyz

where `<DOWNLOADS>` is the directory containing the downloaded file.

See the [virtualenv documentation][DOCS] for help on installing `virtualenv`
more permanently.


Use `virtualenv` to create a directory including `pip`
------------------------------------------------------

Run:

    virtualenv <ENV>

where `<ENV>` is the "virtualenv directory" to create.

You may use something other than `virtualenv`, as suggested in the previous
step.


Use `pip` to install the packages, and any other packages they need
-------------------------------------------------------------------

Run:

    <ENV>/bin/pip install -U <PACKAGE>

where `<ENV>` is the virtualenv directory, `<PACKAGE>` is the package name,
and `bin` should be changed to `Scripts` if you are using Windows.

Alternatively, to install multiple packages, run:

    <ENV>/bin/pip install -U -r requirements.txt

where `requirements.txt` is a list of the packages to install, one per line.

Each package name may be immediately followed (without a space) by a version
specifier such as `==1.2.0` or `>=1.2.0`.  The other details of what can be
put in these files are explained [here][REQS].

[REQS]: https://pip.readthedocs.org/en/stable/user_guide/#requirements-files

If your package fails to install, try updating the `setuptools` and `wheel`
packages and then try again:

    <ENV>/bin/pip install -U setuptools
    <ENV>/bin/pip install -U wheel

The next most common cause of problems is that the package depends on a
working C compiler with the right header files available to it.  This usually
involves installing the right system packages, for instance with
`apt install SYSPACKAGE` on Debian/Ubuntu Linux, which may require searching
the web to find which ones you need.

You can find out what Python package versions have been installed in your
virtualenv directory by running:

    <ENV>/bin/pip freeze


Troubleshooting
---------------

Search the web for the exact error message you're getting.


Conclusion
----------

All being well, you now have a working "virtualenv directory", and can create
more of them as you need them.

You can test it by running:

    <ENV>/bin/python       # Use "<ENV>/Scripts/python" on Windows.

You should then be able to import the modules from the packages you installed
by typing:

```#python
import <MODULE>
```

where `<MODULE>` is an appropriate module name.  (Type `quit()` to exit Python).

You can also run any of the commands in the `bin` or `Scripts` directory, and
they will be able to use the installed packages.

Perhaps you'd like to read the [second part of this guide][PART-2], which
fills in a few more details?

Please raise issues if you have any questions, or if you have ideas for how to
improve this guide.

[PART-2]: virtualenv-guide-part-2.md
