---
layout: page
title: "Setup"
permalink: /setup/
root: ..
---

# Installation Instructions

## Anaconda vs Miniconda vs Miniforge

Anaconda is a distribution of the Conda package manager and a number of other useful packages. Traditionally this lesson recommended installing Anaconda as an easy way to get everything required. Anaconda has changed it's licensing terms and now requires users at [organisations with more than 200 employees to pay for a license](https://www.anaconda.com/pricing/terms-of-service-faqs). This does not apply to "accredited educational institutions" but the policy for institutions which focus on research rather than education is unclear. This restriction also applies to Miniconda and using the defaults software channel in Conda. The Mini Forge distribution has been created as an open source community supported alternative that does not have these license restrictions. To avoid any potential licensing problems it is recommended to use Miniforge for this lesson.

## Check to see if Conda is already installed

If you have ever installed [Miniforge](https://conda-forge.org/download/)
on your local machine, then you already have Conda installed! Mac and Linux users can check 
whether Conda is installed by running the following command in a terminal.

~~~
$ which conda
/Users/$USERNAME/miniforge3/bin/conda
~~~
{: .language-bash}

If Conda has already been installed on your machine, then this command should return the 
absolute path to the conda executable. 

Windows users should search for "Miniforge" to see if the "Miniforge Prompt" shows up as an 
option, if it does then you already have Conda installed.

> ## Old version of Conda?
>
> If you previously installed a Conda distribution you may have an old version of Conda. You
> can check your version of Conda with the following command.
> 
> ~~~
> $ conda --version
> ~~~
> {: .language-bash}
> 
> If you have a version of Conda that is 4.5 (or older), then it is probably best to 
[uninstall](https://docs.anaconda.com/anaconda/install/uninstall/) your Conda distribution 
> and then reinstall a recent version Miniforge.
{: .callout}

## Install Miniforge

If Conda has not been installed on your machine, then install [Miniforge](https://conda-forge.org/download/) for your OS. As the name 
suggests, Miniforge is a "mini" version of the 
[Anaconda Python distribution](https://www.anaconda.com/distribution/) that includes only Conda, a 
Python 3 distribution, and any necessary OS-specific dependencies. 

For convenience here are links to the 64-bit Miniconda installers.

* [Windows](https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Windows-x86_64.exe)
* [Mac OSX - Intel CPU](https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-MacOSX-x86_64.sh)
* [Mac OSX - Apple M1/2/3 CPU](https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-MacOSX-arm64.sh)
* [Linux](https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh) 


### Windows installation

After you downloaded the [Windows installer](https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Windows-x86_64.exe), double click on it and follow the instructions (accept license, etc.).
Make sure you tick on **"Add Miniforge3 to my PATH environment variable"** option.

### Mac OSX or Linux installation

First, download the 64-bit Python 3 install script for Miniforge
either by clicking the link above or using this command in your terminal:

~~~
wget "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
~~~
{: .language-bash}

Run the Miniforge install script from your terminal. Follow the prompts on the installer screens. If you are unsure 
about any setting, accept the defaults (you can change them later if necessary).

~~~
bash Miniforge3-$(uname)-$(uname -m).sh
~~~
{: .language-bash}

Once the install script completes, you can remove it.

~~~
rm Miniforge3-$(uname)-$(uname -m).sh
~~~
{: .language-bash}

## Verifying your Conda installation

In order to verify that you have installed Conda correctly run the `conda help` command. Output 
of the command should look similar to the following.

~~~
$ conda help
usage: conda [-h] [-V] command ...

conda is a tool for managing and deploying applications, environments and packages.

Options:

positional arguments:
  command
    clean        Remove unused packages and caches.
    config       Modify configuration values in .condarc. This is modeled
                 after the git config command. Writes to the user .condarc
                 file (/Users/drpugh/.condarc) by default.
    create       Create a new conda environment from a list of specified
                 packages.
    help         Displays a list of available conda commands and their help
                 strings.
    info         Display information about current conda install.
    init         Initialize conda for shell interaction. [Experimental]
    install      Installs a list of packages into a specified conda
                 environment.
    list         List linked packages in a conda environment.
    package      Low-level conda package utility. (EXPERIMENTAL)
    remove       Remove a list of packages from a specified conda environment.
    uninstall    Alias for conda remove.
    run          Run an executable in a conda environment. [Experimental]
    search       Search for packages and display associated information. The
                 input is a MatchSpec, a query language for conda packages.
                 See examples below.
    update       Updates conda packages to the latest compatible version.
    upgrade      Alias for conda update.

optional arguments:
  -h, --help     Show this help message and exit.
  -V, --version  Show the conda version number and exit.

conda commands available from other packages:
  env
~~~
{: .language-bash}

At the bottom of the help menu you will see a section with some optional arguments for the 
`conda` command. In particular you can pass the `--version` flag which will return the version 
number. Again output should look similar to the following.

~~~
$ conda --version
conda 4.8.2
~~~
{: .language-bash}

## Make sure you have the most recent version

Once Conda exists on your machine, then run the following command to make sure that you 
have the most recent version and patches.

~~~
$ conda update --name base --channel defaults --yes conda
~~~
{: .language-bash}

You can re-run this command at any time to update to the most recent version of Conda.

## Initializing your shell for Conda

Key parts of Conda's functionality require that it interact directly with the shell within which 
Conda commands are being invoked as such each shell must be configured to make use of them. The 
`conda init` command initializes a shell for use with Conda by making changes to your system that 
are specific and customized for each shell. Conda supports a number of different shells and you 
can run `conda init --help` to see the complete list.

Mac OSX and Linux users will want to initialize Conda for Bash as follows. If you are installing 
on Linux, then you may be prompted to initialize Conda for your shell when running the installation 
script. If so, then you can safely skip this step.

~~~
$ conda init bash
~~~
{: .language-bash}

Windows users can use the Miniforge Prompt which 
are already initialized for Conda or they can initialize Conda for Powershell as follows.

~~~
> conda init powershell
~~~

After running `conda init` you will need to close and restart your shell for changes to take 
effect. Alternatively, Mac OS and Linux users can reload your `~/.bashrc` profile (which was 
changed by running the `conda init` command). To reload your `~/.bashrc` profile, use the 
following command.

~~~
$ source ~/.bashrc
~~~
{: .language-bash}

If you want to reverse or “undo” the changes made by `conda init`, then you can re-run the 
`conda init` command and pass the `--reverse` option. Again, in order for the reversal to take 
effect you will likely need to close and restart your shell session.

## Use of Binder instead of installing Conda (Optional)

If you wish to get started with this course without installing Conda, then you can use a 
pre-configured instance running on [Binder](https://mybinder.org/) by clicking on the link below.

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/carpentries-incubator/introduction-to-conda-for-data-scientists/binder?urlpath=lab)

## Workspace for Conda environments

In order to maintain a consistent workspace for all your conda environment, we will create a new
`introduction-to-conda-for-data-scientists` directory on your Desktop and store our conda environment in this directory.
On Mac OSX and Linux running following commands in the
Terminal will create the required directory on the Desktop.

~~~
$ cd ~/Desktop
$ mkdir introduction-to-conda-for-data-scientists
$ cd introduction-to-conda-for-data-scientists
~~~
{: .language-bash}


For Windows users you may need to reverse the direction of the slash and run 
the commands from the command prompt.

~~~
> cd ~\Desktop
> mkdir introduction-to-conda-for-data-scientists
> cd introduction-to-conda-for-data-scientists
~~~
{: .language-bash}

Alternatively, you can always "right-click" and "create new folder" on your Desktop. All the 
commands that are run during the workshop should be run in a terminal within the 
`introduction-to-conda-for-data-scientists` directory.
