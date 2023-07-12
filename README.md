# Using Conda

How to install Conda to use the group's tools and codes.

----

Conda is a package management system suitable for Python packages and also for many scientific codes, not necessarily written in Python (for example, Packmol and Gnuplot are available as Conda packages). Conda manages dependencies, meaning it installs all that is required for a given software to run and tries to keep all those packages updated while ensuring compatibility of versions.

## 0 For the impatient

Download a [Miniconda installer archive](https://docs.conda.io/en/latest/miniconda.html#installing)

    bash Miniconda3-latest-XXX-XXX.sh

    conda activate
    conda config --append channels conda-forge
    conda install numpy matplotlib jupyter lmfit

You are ready to use (most of) the group's Python tools.


----

## 1 Install a Conda distribution

I recommend [Miniconda](https://docs.conda.io/en/latest/miniconda.html), which starts as a smaller installation. Packages are then installed as needed.

In the [Installing](https://docs.conda.io/en/latest/miniconda.html#installing) section choose the archive corresponding to your platform. On Mac I use the bash archive and then in a terminal do:

    bash Miniconda3-latest-XXX-XXX.sh

This creates a `miniconda3` folder in your home dir, and also asks to modify your shell configuration files to enable activation of the conda environment (you'll have to close and reopen your terminal shell).

If conda is not activated automatically you can do that with

    conda activate

To exit the conda environment type

    conda deactivate

(If you have other Python installations in your computer outside Conda, for example with Homebrew or Pip, it is advisable to manage those installations while Conda is deactivated.)

## 2 Channels

Channels are repositories of packages. The `defaults` channel contains the large set of Anaconda packages and is sufficient for many uses. It is the channel configured by default.

For scientific computing the `conda-forge` channel should be added:

    conda config --append channels conda-forge

You can check your configuration of channels:

    conda config --show channels

You can change the order of priority, see [Managing channels](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-channels.html).


## 3 Installing and updating packages

The command to install packages is

    conda install numpy
    conda install matplotlib

To search for packages (in the available channels):

    conda search lmfit

You can see the packages already installed with

    conda list

To keep packages up-to-date use the following command regularly:

    conda upgrade --all


## 4 Environments

Environments allow different groups of packages to exist in separate spaces. This is useful for large packages that have many dependencies, which easily give rise to conflicts between versions of certain packages.

The default environment is called `base`. I recommend using the `base` environment for the essential Python packages such as `numpy`, `matplotlib`, `pandas` or `jupyter`. These, together with `lmfit` and maybe a few more tools, are enough to run the group's Python scripts.

If you will *not* be using large computational codes, working only in the `base` environment should suffice and you can skip the rest of this section.

If you will be using large packages (OpenMM, Psi4) then I recommend creating a separate environment for each one. For example,

    conda create --name omm

You can list your different environments with

    conda env list

Then install packages in your active environment as usual.

To activate or deactivate the environment you want to work in:

    conda activate omm

    conda deactivate

(you will be back in `base`).


## 5 Conda and Pip

Conda and Pip are two different package management systems, and a certain discipline is required to avoid confusions. It is possible to install Pip inside a Conda environment and then packages from the PyPi repository. However, this is not an optimal setup and should be avoided if possible (Pip doesn't know about Conda dependencies). Instead, it is advisable to install packages from `conda-forge` and only resort to Pip packages as a last option.

Pip can also reside outside Conda (this is common in a Linux system or in MacOS with Homebrew). In this case it is advisable to deactivate Conda before installing or updating Pip packages.
