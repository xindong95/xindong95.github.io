---
title: "How to configure a bioinformatics environment"
layout: single
comments: true
categories:
  - blogs
  - bioinformatics
tags:
  - software
---

Installing bioinformatics software is often the first obstacle for beginners. However, even experienced users can face errors or warnings when installing new tools or trying new methods. Some old packages that are still needed for work - regenerate their paper's results or use their subfunctions - can be extremely difficult to install. Here’s how I configure my working environment.

> P.S. Since I use macOS and Linux in my daily work, I'll explain these two systems more clearly. Maybe later, I will add Windows as well.  

A package manager is very helpful for your work. It can help you with package versioning, installation, uninstallation, environment variables, and more. Homebrew, Conda, and NPM are all great package managers. They are similar to app stores on your smartphone. Homebrew is a general-purpose software manager that is mostly used on macOS. NPM is a package manager for Javascript. Conda has become a new standard for bioinformatics software. If a new bioinformatics software does not have a conda version, I would think that it might be hard to install and uninstall completely later.  

When you look for conda on google or other search engines, you will see two results: anaconda and miniconda.  

> Conda is an open source package management system and environment management system for installing multiple versions of software packages and their dependencies and switching easily between them. It works on Linux, OS X and Windows, and was created for Python programs but can package and distribute any software.  

Anaconda is a Python distribution that includes many packages related to scientific computation. Miniconda only includes the package manager, and you can install other packages later.  

![python packge](/assets/images/posts_images/2020-09/python-package.png)

You can easily download miniconda here: [https://docs.conda.io/en/latest/miniconda.html](https://docs.conda.io/en/latest/miniconda.html)  

Most computers nowadays have a 64-bit system installed, so choose the 64-bit version installation scripts to download. Python 2.X was deprecated in January 2020, so select the Python 3.x version and use it in the future. On macOS or Linux, I prefer downloading the bash (*.sh) file. Then type `bash Miniconda3-latest-*-x86_64.sh` in the terminal and follow the instructions. It will ask you to give a path where miniconda will be installed. When you are almost finished with the installation, conda will ask you whether you want to initialize conda. Type `yes` to confirm this. It will add several lines of code in your `~/.bashrc` (Linux) or `~/.bash_profile` (macOS) to initialize conda base environment when you log in to the terminal every time. If you typed `no`, you can find where conda is - you set it before - then type `path_to_conda/conda init` to initialize conda. After all of that, you will have miniconda installed.  

You can use conda commands to build your environment. Here are the instructions:  

I suggest using an independent environment for each project to avoid conflicts with different packages. To create a new conda environment, use `conda create -n env_name`. You can also specify the Python version here, e.g., `conda create -n env_name python=2.7`.


```md
conda is a tool for managing and deploying applications, environments and packages.

Options:

positional arguments:
  command
    clean        Remove unused packages and caches.
    compare      Compare packages between conda environments.
    config       Modify configuration values in .condarc. This is modeled
                 after the git config command. Writes to the user .condarc
                 file (/mnt/Storage/home/dongxin/.condarc) by default.
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
  server
```  

You can switch between the environments with `conda activate env_name` and `conda deactivate`. And you can install packages by `conda install`. You also can search whether a package has a conda distribution here: [https://anaconda.org](https://anaconda.org).  

Conda has many channels that collect a category of packages, like conda-forge, bioconda, r, etc. You can create your own channel with your packages as well. Conda can install most of the packages that you need. For example, you can install R by conda install -c conda-forge r-base.

![conda r base](/assets/images/posts_images/2020-09/conda-r-base.png)

Conda is a powerful tool for building environments and handling most of the tricky things in environment configuration. However, solving environment issues can sometimes take a lot of time and can be frustrating when errors occur. At least it is very useful. When building pipelines with Snakemake, it suggests good compatibility with many packages.

Highlight it as a checklist:

- Download miniconda [here](https://docs.conda.io/en/latest/miniconda.html)
- Install miniconda
- Initialize conda with `conda init`
- Build environment with `conda create`
- Install packages you need with `conda install`
- Enjoy

Here are some software that bioinformaticians use and you may interest in as well. Besides, all of them can be installed by conda:  

- bwa (A mapping software)
- macs2 (Used for peak calling)
- STAR (A slice-aware mapping software)
- DESeq2 (An R package for differential expression analysis)
- bedtools (Useful tool to manipulate .BED file)
- samtools (Useful tool to manipulate .BAM/.SAM/.CRAM file)
- Seurat (An R package to analysis single-cell data)

Have a try with the above and tell me any feedback in the comments.

------

I wrote this blog because I encountered a lot of errors when I tried to update R in my base environment. The issue might be related to [this](https://github.com/conda/conda/issues/9367). No matter if I ran `conda install -c conda-forge r-base=4.0` or `conda update -c conda-forge r-base`, the errors and conflict warnings kept showing up.  Finally, I realized that the problem was that I had switched to another conda mirror before. When I tried to update software from the official sources, it conflicted with the previous mirror. After I uninstalled all software from the third-party mirror, the R packages were updated successfully.

![conda tsinghua conflict](/assets/images/posts_images/2020-09/conda-tsinghua-conflict.png)  
