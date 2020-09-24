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

For green hands to bioinformatics, how to install software always is the first obstacle to overcome. In fact, not only newbies meet this problem, but also seniors meet errors or warnings (often ignored) when install new tools or try new methods. Remarkably, some old packages you still need in your work - regenerate their paper's results or use their subfunctions - are extremely difficult to install. Here I would like to suggest how I configure my work environment.  

> P.S. Since I use macOS and Linux in my daily work, I'll explain these two systems more clearly. Maybe later, I will add Windows as well.  

First of all, a package manager is quite useful in your work. It helps you manage package version, install and uninstall, add environment variables, and so on. Homebrew, Conda even NPM are all excellent package managers. They are quite like app stores on your smartphone. Homebrew not very specific to bioinformatics but universal software and most used in macOS. NPM is a package manager specific to Javascript. Conda has become a new standard for bioinformatics software. If a new bioinformatics software does not provide a conda version, the first opinion that comes to me is that it might be hard to install and uninstall thoroughly in the future.  

When you search conda on google or other searching engines, here comes two results: anaconda and miniconda.  

> Conda is an open source package management system and environment management system for installing multiple versions of software packages and their dependencies and switching easily between them. It works on Linux, OS X and Windows, and was created for Python programs but can package and distribute any software.  

The anaconda is regard as a python branch with many packages related to scientific computation. The miniconda only contains the package manager, which means that you can install other packages later.  

![python packge](/assets/images/posts_images/2020-09/python-package.png)

You can easily download miniconda here: [https://docs.conda.io/en/latest/miniconda.html](https://docs.conda.io/en/latest/miniconda.html)  

Nowadays, most computers have already installed a 64-bit system, so choose the 64-bit version installation scripts to download. Python 2.X has deprecated in 2020 January, so select the Python 3.x version and use it in the future. On macOS or Linux, I prefer downloading the bash(*.sh) file. Then type `bash Miniconda3-latest-*-x86_64.sh` in the terminal and follow the instruction. It requires you give a path where miniconda will be installed. When you almost finished installation, conda will ask you whether you want to initialize conda. Type `yes` to confirm this. It will add several lines of codes in your `~/.bash_rc`(Linux) or `~/.bash_profile`(macOS) to make sure initialize conda base environment when you login terminal every time. If you typed `no`, you can find where the conda is - you set it before - then type `path_to_conda/conda init` to initialize conda. After all of those, you get miniconda installed.  

Then you can use the conda commands to build your environment. I paste the instruction below. I suggest that use an independent environment for each project, which avoids conflicts with different packages. To create a new conda environment, use `conda create -n env_name`. You also can specify python version here, e.g. `conda create -n env_name python=2.7`  

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

Conda has many channels that collect a catagory of packges, like conda-forge, bioconda, r, etc. You can create your own channel with your packages as well. Conda can install most of packages that you need. Like R, you can search it on [website](https://anaconda.org) then install it by `conda install -c conda-forge r-base`.  

![conda r base](/assets/images/posts_images/2020-09/conda-r-base.png)

Conda is s powerful tool to build environment and handle almost tricky things in the environment configuration. However, solving environment sometimes costs a lot of time and pops some error that makes me frustrated. At least, it pretty useful. When I build pipelines with snakemake, it suggests good compatibility with many packages.  

To make it as a checklist:

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

The reason I wrote this blog is that I met a bunch of errors when I try to update R in my base environment. The issue may be related to [this](https://github.com/conda/conda/issues/9367). Whatever I run `conda install -c conda-forge r=4.0` or `conda update -c conda-forge r`, the errors and conflict warning shows up endlessly. At last, I figure out the reason is that I have changed to another conda mirrors before. When I try to update software from the official sources, it conflicts with the previous mirror. After I uninstall all software from the third-party mirror, the R packages finally were updated successfully.

![conda tsinghua conflict](/assets/images/posts_images/2020-09/conda-tsinghua-conflict.png)  
