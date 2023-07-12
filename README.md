# tutorial-conda

How to install Conda for the group's tools and codes

----

Conda is a package management system that is suitable to install Python software and also other scientific software packages, not necessarily written in Python (for example `packmol` or `gnuplot` are available as conda packages). Conda manages dependencies, so it installs all that is required for a given software to run and can keep all those packages updated.

## 1 Install a conda distribution

I recommend [`Miniconda`](https://docs.conda.io/en/latest/miniconda.html), which starts as a smaller installation. Packages are then installed as needed.

In the [Installing](https://docs.conda.io/en/latest/miniconda.html#installing) section choose the archive corresponding to your platform. On Mac I use the bash archive and then in a terminal do:

        bash Miniconda3-latest-MacOSX-x86_64.sh

This creates a `miniconda3` folder in your home dir, and also modifies your shell configuration files to enable activation of the conda environment (you'll have to close and reopen your shell terminal).

If conda is not activated automatically you can do it with

        conda activate

To exit the conda environment type

        conda deactivate

If you have other Python installations in your computer outside conda (for example with `Homebrew` or `pip`) it is advisable to manage those installations while conda is deactivated.

## 2 Channels

Channels are repositories of packages. The `defaults` channel contains the large set of Anaconda packages and is sufficient for many uses. It is the channel configured by default.

For scientific computing the `conda-forge` channel should be added:

        conda config --append channels conda-forge

You can check your configuration of channels:

        conda config --show channels

The order of priority can be different, see [Managing channels](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-channels.html)


## 3 Installing and updating packages

THe command to install packages is

        conda install numpy
        conda install matplotlib

To search for packages (in the available channels):

        conda search lmfit

You can see the installed packages with

        conda list

To keep packages up-to-date:

        conda upgrade --all



## 4 Environments

Environments allow different groups of packages to exist in separate spaces. This is useful for large packages that have many dependencies, which easily give to conflicts between versions.

The default environment is called `base`. I recommend using the `base` environment for commonly used tools and small packages. Essential Python packages such as `numpy`, `matplotlib`, `pandas`, `jupyter` can be installed in the `base` environment. These, together with `lmfit` and maybe a few more tools, are enough to run the group's Python scripts.

If you are not using large computational codes you can skip the rest of this section.

If you will be using large packages (OpenMM, Psi4) then I recommend that you create a separate environment for each one. For example,

        conda create --name omm

Then install packages in the active environment as usual.

You can activate and deactivate the environment you want to work in:

        conda activate omm

        conda deactivate


## 5 Conda and Pip

Conda and pip are two different package management systems, and a certain discipline is required to avoid confusion. It is possible to install pip inside a conda environment and then packages from the PyPi repository. However, this is not a good setup and should be avoided if possible. It is advisable to install packages from `conda-forge` instead and only resort to pip as a last option.
