---
title: Python virtual environments
excerpt: Keep your python environment clean!
comments: true
header:
  overlay_image: header.png
---

# What is virtualenv?

As you work on Python projects, you need to install the packages you depend on, e.g. `numpy`, `sqlalchemy`, `flask`, etc.
Using a single Python environment for all of your projects can be  problematic for a few reasons:

1. You might have two different projects which require different versions of the same library.

1. You might have projects which use different versions of Python!

1. If you're importing stuff from a source repo in one of your projects, you might want to add that source repo to the `PYTHONPATH` for that project, but not for others.

Fortunately, the python community has invented [`virtualenv`](https://virtualenv.pypa.io/en/stable/), i.e. "virtual environments" to make this situation better.
Each project you work on gets its own virtualenv and when you install packages in a virtualenv, they apply only to that virtualenv and therefore only to that project.
When creating a virtualenv, you can even pick the version of python you'd like to use!

Creating and using virtualenvs is pretty easy, but there's another package called [`virtualenvwrapper`](https://virtualenvwrapper.readthedocs.io/en/latest/) which makes managing and switching between virtualenvs even easier.

In this post, we give the basic steps to set up `virtualenv` and `virtualenvwrapper`.
For complete, detailed, step-by-step instructions, see [my writeup on Google Drive](https://docs.google.com/document/d/1hXM_noMrsp1LTic_jSbgHHr5a2rwmI3b7DZdoo9IYGo/).

# Install virtualenv and virtualenvwrapper

## Linux

We'll use commands from Ubuntu.
If you're on a different Linux distribution, substitute the appropriate package manager command wherever you see `apt-get`.
Anything starting with a `$` is a shell command.

```
$ sudo apt-get install virtualenvwrapper
```

Edit your `.bashrc` file by adding the following three lines

```
export WORKON_HOME=$HOME/.virtualenvs
export PROJECT_HOME=$HOME/src
source /usr/share/virtualenvwrapper/virtualenvwrapper.sh
```

Restart your shell to pick up the changes to `.bashrc`.
`virtualenvwrapper` is now installed.

# Basic virtualenvwrapper commands

* `$ mkvirtualenv <virtual env name>`:  make a new virtualenv named `<virtual env name>`.

* `$ workon <virtual env name>`: activate an existing virtualenv.

* `$ deactivate`: deactivate the virtualenv you're on.

# Install packages in a virtualenv

Once you have a virtualenv activated, simply `pip install <python package>` to install a package into that virtualenv.
Note that because we put our virtualenvs in our home directory, we don't need `sudo` to install python packages!

# Resources

For more details, see the Google doc linked above.

In a future post, I will give a detailed explanation of how to install PyQt in a virtualenv, since it doesn't work with pip.

