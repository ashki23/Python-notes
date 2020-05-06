# Virtual environments in Python
*[Ashkan Mirzaee](https://ashki23.github.io/index.html)*

"Python applications will often use packages and modules that don’t come
as part of the standard library. Applications will sometimes need a
specific version of a library, because the application may require that
a particular bug has been fixed or the application may be written using
an obsolete version of the library’s interface.

This means it may not be possible for one Python installation to meet
the requirements of every application. If application A needs version
1.0 of a particular module but application B needs version 2.0, then the
requirements are in conflict and installing either version 1.0 or 2.0
will leave one application unable to run.

The solution for this problem is to create a virtual environment, a
self-contained directory tree that contains a Python installation for a
particular version of Python, plus a number of additional packages." -
from [the Python Tutorial](https://docs.python.org/3/tutorial/venv.html)

In this tutorial we will discuss about two major methods to create and
manage virtual environments in Python.

-----

## Venv

To create a virtual environment, run the venv module as a script with
the directory path. For example the following code uses the venv module,
`-m venv`, to create `tutorial-env` in the current directory:

``` bash
python3 -m venv tutorial-env
```

It also creates directories containing a copy of the Python interpreter,
the standard library, and various supporting files. Once we’ve created a
virtual environment, we can activate it by:

``` bash
source tutorial-env/bin/activate
```

After activating the environment with the above command, we can use
`pip` to install required packages by:

``` bash
pip install <package name>
```

For example, the following Bash scripts creates `tutorial-env` if it
does not exist, and upgrade `pip` and install modules after activation:

``` bash
#!/bin/bash

if [ ! -d tutorial-env ]; then
  python3 -m venv tutorial-env
fi

source tutorial-env/bin/activate

pip install --upgrade pip
pip install redis
pip install gitpython
```

As a shortcut, we can use `.` instead of `source`. To exit from a
virtual environment run `. deactivate`.

## Miniconda

To use a more sophisticated method, we might consider Conda as an
environment management system. To start using Conda, you might need to
install Miniconda (or Anaconda) first. Follow the instruction at [Conda
website](https://conda.io/projects/conda/en/latest/user-guide/install/index.html)
to install Miniconda (or Anaconda) on the operating system.

To create a new environment, use `conda create` command including names
of the environment and required packages:

``` bash
conda create --name <env_name> <pkg name> <pkg name> ...
```

We also can use `--yes` flag to set up the environment without a
question and use `--prefix <env_path>` to setup the environment in a
certain path (note that we can not use `--prefix` and `--name` at the
same time). To see list of environments, use the following:

``` bash
conda env list
```

We can also use `conda info --envs` to see list of envs. To
activate/deactivate an environment use the following:

``` bash
conda activate <env_name or env_path>
conda deactivate
```

Note that, for Conda versions prior to 4.6 we need to use `source`
instead of `conda` in the above commands. Now, use the following to
update `conda` and install a new package:

``` bash
conda update conda
conda install <pkg name>
```

To remove the package use:

``` bash
conda remove <pkg name>
```

To see list of the installed packages within the env, use:

``` bash
conda liat
```

And to remove cache files use:

``` bash
conda clean --all
```

**Note**: before removing packages or caches, make sure we are in the
right virtual environment. We can use `conda info` and `conda env list`
to find the current environment and use `source activate <env name or
path>` or `source deactivate` to active or deactivate the right env.

To remove a virtual environment use:

``` bash
conda env remove --name <env_name> or --prefix <env_path>
```

**Note**: we cannot remove an environment when it is activate. Sometime,
an env should `deactivate` multiple times, if it is activated more than
once.

To prevent dependencies crash, it is vital to install all the packages
at the same time (if possible) when a new environment is creating by
listing all packages listed after env directory in `cond create`. Also,
it is very important to name all channels (which are not in the standard
channels that conda searches by default) the are required. For example
if one of the packages is in channel `r` and another in `conda-forge`
then use:

``` bash
conda create --channel r --channel conda-forge --prefix ./yourlocal_env <pkg name> <pkg name> <pkg name> ...
```

Also, it is important to keep using same channels for updating the
environment by:

``` bash
conda update --chanel r --channel conda-forge --prefix ./yourlocal_env <pkg name> <pkg name> ...
```

In a **HPC** cluster system, first we need to load `miniconda3` module
to be able to use `conda`. We can use the following as a template to
build new environment:

``` bash
export CONDA_PKGS_DIRS=<dir>/.conda/pkgs
export CONDA_ENVS_PATH=<dir>/.conda/envs
module load miniconda3

if [ ! -d yourlocal_env ]; then
conda create --yes --prefix ./yourlocal_env <pkg name> <pkg name> ...
fi
source activate ./yourlocal_env
```

We need to update conda pathes (`CONDA_PKGS_DIRS` and
`CONDA_ENVS_DIRS`), only if we prefer to put them somewhere except home
directory.

---

Copyright 2018-2019, [Ashkan Mirzaee](https://ashki23.github.io/index.html) | Content is available under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | Sourcecode licensed under [GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)
