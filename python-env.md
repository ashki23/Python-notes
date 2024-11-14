# Virtual environments in Python

“Python applications will often use packages and modules that don’t come
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
particular version of Python, plus a number of additional packages.” -
from [the Python Tutorial](https://docs.python.org/3/tutorial/venv.html)

In this tutorial we will discuss about two major methods to create and
manage virtual environments in Python.

------------------------------------------------------------------------

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
pip install <package1> <package2=version> <package3>=version> ...
```

For example, the following Bash script creates `tutorial-env` if it does
not exist, and install `redis` and `gitpython` after activation:

``` bash
#!/bin/bash

if [ ! -d tutorial-env ]; then
  python3 -m venv tutorial-env
fi

source tutorial-env/bin/activate
pip install redis gitpython
```

To uninstall packges use:

``` bash
pip unisntall <package1> <package2> ...
```

To keep a list of the packages (commonly called `requirements.txt`) that
are installed in the env, use:

``` bash
pip freez > requirements.txt
```

To install packages from a `requirements.txt` file use:

``` bash
pip install -r requirements.txt
```

We can use `deactivate` command to deactivate and env and use
`rm -rf <env_path>` to remove th env.

------------------------------------------------------------------------

## Miniconda

To create virtual environments, [Conda](https://conda.io/en/latest/)
could be the best environment management system. Miniconda is an open
source package and environment management system that includes Conda.
Conda quickly installs, runs and updates packages and their
dependencies. To start using Conda, follow the instruction in
[here](https://conda.io/projects/conda/en/latest/user-guide/install/index.html)
to install Miniconda (or Anaconda if you want to have most of the
scientific packages) on your operating system.

When Miniconda is installed, use `conda init <shell-name>` to initiate
Conda and run `conda config --set auto_activate_base false` to stop auto
base activation. We can also use `conda update conda` to upate Conda.

For adding Conda autocompletion, in bash terminal copy
[conda-bash-completion](https://github.com/tartansandal/conda-bash-completion/blob/master/conda)
in `/usr/share/bash-completion/completions/conda`. And for a macOS with
zsh, copy
[conda-zsh-completion](https://github.com/esc/conda-zsh-completion/blob/master/_conda)
in `~/miniconda3/zsh-completion/_conda` and add the following to the
`~/.zshrc` file:

``` bash
fpath+="/Users/${USER}/miniconda3/zsh-completion" && compinit
```

### Usage

To create a new environment, use `conda create` command including names
of the environment and required packages:

``` bash
conda create --name <env_name> <package1> <package2=version> ...
# or
conda create --prefix <env_path> <package1> <package2=version> ...
```

We also can use `--yes` flag to set up the environment without a
question. We use `--prefix <env_path>` to setup the environment in a
certain path. Note that we can not use `--prefix` and `--name` at the
same time.

To see list of environments, use the following:

``` bash
conda env list
```

To activate an environment type:

``` bash
conda activate <env_name> or <env_path>
```

Note that, for Conda versions prior to 4.6 we need to use `source`
instead of `conda` to activate an env. Now, use the following to install
new packages in the activated env:

``` bash
conda install <package1> <package2=version> ...
```

To uninstall packages use:

``` bash
conda uninstall <package1> <package2=version> ...
```

To see list of the installed packages within the env, use:

``` bash
conda list
```

To keep a list of the packages (commonly called `requirements.txt`) that
are installed in the env, use:

``` bash
conda list --export > requirements.txt
```

We can deactivate the env by:

``` bash
conda deactivate
```

And remove the deactivated virtual environment by:

``` bash
conda env remove --name <env_name> or --prefix <env_path>
```

To remove cache files we can use:

``` bash
conda clean --all
```

We can regenerate an env from a `requirements.txt` file:

``` bash
conda create --name <env_name> --file requirments.txt
```

Note that there is a short form for most of the Conda options that can
be used instead of the long form. For instance, `-n`, `-p`, `-c`, `-y`,
and `-e` can be used instead of `--name`, `--prefix`, `--channel`,
`--yes`, and `--export`, respecively. You may find more information by
using `conda -h` or `conda <command> -h`.

### Conda channels

Whenever we use `conda create` or `conda install` without mentioning a
channel name, Conda package manager search its default channels to
install the packages. If you are looking for specific packages that are
not in the default channels you have to mention them by using:

``` bash
codna create --name <env_name> --channel <channel1> --channel <channel2> ... <package1> <package2> ...
```

For example the following creates `new_env` and installs r-sf, shapely
and bioconductor-biobase from `r`, `conda-forge` and `bioconda`
channels:

``` bash
codna create --name new_env --channel r --channel conda-forge --channel bioconda r-sf shapely bioconductor-biobase
```

Ideally, you should create one environment per project and include all
the required packages when you create the environment and try to use a
single channel as much as possible. It is important using the same
channels for updating the environment.

### Conda packages

To find the required packages, we can visit
[anaconda.org](https://anaconda.org) and search for packages to find
their full name and the corresponding channel. Another option is using
`conda search` command. Note that we need to search the right channel to
find pakages that are not in the default channels. For example:

``` bash
conda search --channel bioconda biobase
```

### HPC workflow

In a HPC cluster system, first we need to load `miniconda3` module to be
able to use `conda`. We can use the following as a template for building
a new environment:

``` bash
module load miniconda3

if [ ! -d <env_path> ]; then
conda create --yes --prefix <env_path> <package1> <package2> ...
fi
source activate <env_path>
```

To keep Conda packages and caches somewhere except the home directory,
we can update conda pathes by exporting new `CONDA_PKGS_DIRS` and
`CONDA_ENVS_DIRS` or creating/updating `~/.condarc` file. Review
[here](https://docs.conda.io/projects/conda/en/latest/user-guide/configuration/use-condarc.html#specify-environment-directories-envs-dirs)
to learn more.

---

Copyright, [Ashkan Mirzaee](https://ashki23.github.io/index.html) | Content is available under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | Sourcecode licensed under [GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)
