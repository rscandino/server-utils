# Virtual Environments with Conda and Mamba

The adoption of virtual environments is an essential practice in the management of scientific and development projects, especially when using languages like
Python. Although virtual environments are extremely common in the Python ecosystem (with tools like `virtualenv`, `pyenv`, and `venv`), the use of solutions
like [Conda](https://docs.conda.io/en/latest/) offers a more comprehensive approach that extends beyond simple environment management.

The main advantage of Conda over other environment managers is its dual functionality: it acts as both a **package manager** and a **dependency resolver**. This
means it automatically handles libraries and their dependencies, unlike tools such as `venv`, which delegate dependency management to `pip`.

Moreover, using Conda environments increases the reproducibility or your work thanks to **environments isolation**, **dependency management**, and **environment
files**.

## What Are Virtual Environments?
Virtual environments are essentially isolated directories, each containing its own installation of Python and an independent set of packages. A virtual
environment is built on top of an existing base installation and can be configured to be completely isolated from it. The primary benefit of using a virtual
environment is the ability to have different versions of a package installed on the same system without them conflicting. For example, one project might require
a specific version of a library, while another project requires a different one. Without virtual environments, installing packages for one project could break
the other.

## Advantages of Conda and Mamba
Conda stands out for its ability to manage both packages and environments, intelligently resolving dependencies between libraries. This is particularly
advantageous for projects that require complex libraries or specific software versions, as it prevents compatibility errors. 

[Mamba](https://mamba.readthedocs.io/en/latest/installation/mamba-installation.html), a high-speed implementation of Conda, offers an even more efficient user experience. It uses a dependency resolution logic written in C++ that significantly speeds up the creation and updating of environments. For the user, Mamba's commands are identical to Conda's, making the transition easy and intuitive.

## Up a Conda/Mamba Environment

### Step 1: Installing Conda from Conda-Forge (with mamba built in)
If Conda is not already installed on the server, you need to install the lightweight version, Miniconda.

```shell
# Download the installer (check the Conda website for the latest version
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh

# Run the installer 
bash Miniconda3-latest-Linux-x86_64.sh 

# source bashrc to start Conda 
source ~/.bashrc 

# Init both conda and mamba config 
conda init 
mamba init --all

```

### Step 3: Creating a New Environment
To create an isolated environment, use the create command. Give the environment a descriptive name and specify the initial package versions, such as Python.

```shell
conda create --name my_project python=3.10
# Or with Mamba, which is much faster
mamba create --name my_project python=3.10
```

### Step 4: Activating the Environment
To work inside your new environment, you must activate it. The terminal prompt will change, indicating the active environment.

```shell
conda activate my_project
```

### Step 5: Installing Packages
Once the environment is activated, you can install the packages needed for your work.

```shell
conda install numpy pandas scikit-learn
# Or, for a faster installation:
mamba install numpy pandas scikit-learn
```

### Step 6: Deactivating and Removing the Environment 
Once your work is finished, deactivate the environment to return to the base environment.

```shell
conda deactivate
# or using mamba
mamba deactivate
```

If an environment is no longer needed, you can remove it to free up disk space.

```shell
conda remove --name my_project --all
```

### Step 6: Remember to clean your Conda/Mamba cache
Conda/Mamba tend to keep save sources of downloaded packages, even when they are not useful anymore. Clean them by running

```shell
conda clean --all
# or with mamba
mamba clean -- all
```
