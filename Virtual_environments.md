# Virtual Environments in Python
[The Python Tutorial](https://docs.python.org/3/tutorial/venv.html)

Python applications will often use packages and modules that don’t come as part of the standard library. Applications will sometimes need a specific version of a library, because the application may require that a particular bug has been fixed or the application may be written using an obsolete version of the library’s interface.

This means it may not be possible for one Python installation to meet the requirements of every application. If application A needs version 1.0 of a particular module but application B needs version 2.0, then the requirements are in conflict and installing either version 1.0 or 2.0 will leave one application unable to run.

The solution for this problem is to create a virtual environment, a self-contained directory tree that contains a Python installation for a particular version of Python, plus a number of additional packages.

## venv
To create a virtual environment, decide upon a directory where you want to place it, and run the venv module as a script with the directory path:
```bash
python3 -m venv tutorial-env
```

This will create the `tutorial-env` directory if it doesn’t exist, and also create directories inside it containing a copy of the Python interpreter, the standard library, and various supporting files. Once you’ve created a virtual environment, you may activate it by:
```bash
source tutorial-env/bin/activate
```

We can use the following Bash scripts to create `tutorial-env` if it does not exist and activate it and install modules:
```bash
#!/bin/bash

if [ ! -d tutorial-env ]; then
  python3 -m venv tutorial-env
fi

source tutorial-env/bin/activate

pip install --upgrade pip
pip install redis
pip install gitpython
```

As a shortkey, you might use `.` instead `source`. To exit from a virtual environment run `deactivate`. 

## Miniconda
To use use Conda as an environment management system, you need to install Miniconda (or Anaconda) and use `conda create` to make a new environment by:
```bash
conda create --name <env_name> <pkg name> <pkg name> ...
```

You also can use `--yes` flag to set up the environment without a question and use `--prefix <env_path>` to setup the environment in the path that you want (note that you can not use `--prefix` and `--name` at the same time). To see list of environments, use the following:
```bash 
conda env list
```

You might also use `conda info --envs` to see list of envs. To activate/deactivate an environment use the following:
```bash
conda activate <env_name or env_path>
conda deactivate
```

Note that, for conda versions prior to 4.6 you need to use `source` instead of `conda` in the above commands. Now, you can use the following to update `conda` and install new libraries and software:
```bash
conda update conda
conda install <pkg name>
```

To remove a package you can use:
```bash 
conda remove <pkg name>
```

And to remove cache files use:
```bash
conda clean --all
```

**Note**: before removing packages or caches, make sure you are in the right virtual environment. You can use `conda info` and `conda env list` to find your current environment and use `source activate <env name or path>` or `source deactivate` to go to the rigth env.

To remove a virtual environment you can use:
```bash
conda env remove --name <env_name> or --prefix <env_path>
```
**Note**: you cannot remove an environment when it is activate. Note that sometime you should `deactivate` multiple times, if you `activate` more than once.

In a **HPC** cluster system, first you need to load `miniconda3` module to be able to use `conda`. You can use the following as a template to build your new environment:
```bash
export CONDA_PKGS_DIRS=~/.conda/pkgs
export CONDA_ENVS_PATH=~/.conda/envs
module load miniconda3

if [ ! -d yourlocal_env ]; then
conda create --yes --prefix ./yourlocal_env <pkg name> <pkg name> ...
fi
source activate ./yourlocal_env
```
