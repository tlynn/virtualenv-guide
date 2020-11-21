Handy guide to virtualenv - Part 2
==================================

This extension to the "Handy guide to virtualenv" covers the details which
were omitted to make it shorter.


Inside a virtualenv directory
-----------------------------

The directory created by `virtualenv` contains Python packages and other files
that they need to run.  Inside, it looks like this:

    <ENV>/
        # On Windows, "bin" is called "Scripts"
        bin/     <-- commands
            pip
            python
            ...

        lib/
            site-packages/   <-- installed packages
                ...
        ...

The `bin` or `Scripts` directory contains the `pip` and `python` commands for
installing and running packages, and any other commands that the installed
packages provide.


Activating the virtualenv directory
-----------------------------------

To use a command from the virtualenv directory, you will need to specify its
full path.  So you end up typing, say, `path/to/my/virtualenv/dir/bin/pip`
instead of just `pip`.

To avoid that hassle, you can "activate" the virtualenv, which temporarily
changes your search path to include your `bin`/`Scripts` directory so that
typing `pip` will work.

If you are running on Windows, you just need to run:

    <ENV>/Scripts/activate

On other platforms you usually need to add a ". " (a dot and a space) first:

    . <ENV>/bin/activate

See the [activate documentation][2] if that doesn't work for you, for instance
because you are not running a "bash compatible" shell.

[2]: https://virtualenv.readthedocs.org/en/latest/userguide.html#activate-script


Deactivating the virtualenv directory
-------------------------------------

Run:

    deactivate


Activating the virtualenv directory from Python
-----------------------------------------------

There is also an `activate_this.py` module alongside the `activate` script.
This lets a Python 2 interpreter outside the virtualenv directory gain access
to the modules installed in the directory by using:

    execfile(r'<ENV>/bin/activate_this.py',
             dict(__file__=r'<ENV>/bin/activate_this.py'))

where `<ENV>` is the location of the virtualenv directory and `bin` should be
`Scripts` on Windows.

Python 3 has removed the `execfile` function, and its replacement, the `runpy`
module, doesn't work for this purpose.


About this guide
----------------

This guide tries to be (in rough preference order):

* Secure
* Beginner-friendly
* Correct
* Cross-platform
* Clean (with respect to the rest of your file system)
* Humble (not requiring privileged access such as `root` or `admin`)
* Simple (in its use of language)
* Complete (enough)
* Consistent
* Short

Apologies for where it falls short.

"Secure" may seem a strange top priority, but this is about downloading code
from the internet.  You probably want it to be the right code
([in so far as possible][3]).

[3]: https://caremad.io/2013/07/packaging-signing-not-holy-grail/

Copying this guide is fine with me.  I won't sue.

Please raise issues if you have any questions, or if you have ideas for how to
improve this guide.
