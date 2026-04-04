---
layout: page
title: 🙋‍♂️ Tech Support
description: Pointers on how to solve common technical issues.
nav_order: 4
---

# 🙋‍♂️ Tech Support
{:.no_toc}

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

## Introduction

In DSC 10, you worked on assignments on DataHub, a computing platform that already had all of the Python packages you needed installed. But in the real world, you'll be expected to set up and maintain a Python environment locally – that is, on your own computer – and so that's what we'll have you do here. **That's right – no DataHub!** You already have experience writing and running code locally from DSC 20 and DSC 30; setting up your environment for DSC 80 will be slightly more involved than it was there, but most of these steps only need to be done once.

There has been a lot written about how to set up a Python environment, so we won't reinvent the wheel. This page will only be a summary; Google will be your main resource. But always feel free to come to a staff member's office hours if you have a question about setting up your environment, using Git, or similar — we're here to help.

---

[This video](https://www.loom.com/share/0ea254b85b2745e59322b5e5a8692e91?sid=b77c5c2d-0c24-40fb-8cfc-8574d49d9019) from a previous iteration of the course walks through most of the steps here, but it's **not** a substitute for reading this page carefully.

<div style="position: relative; padding-bottom: 64.92335437330928%; height: 0;"><iframe src="https://www.loom.com/embed/0ea254b85b2745e59322b5e5a8692e91?sid=96bb8188-9783-4878-bc1a-5f6946b20a61" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>

---

## Environments and Package Managers

For this class, the software you'll need includes Python 3.10, a few specific Python packages, Git, and a text editor.

Gradescope has an **environment** which it uses to autograde your work. You can think of an environment as a combination of a Python version and _specific_ versions of Python packages that is isolated from the rest of your computer. In practice, developers create different environments for different projects, so that they can use different versions of packages in different projects.

We're going to have you replicate the environment Gradescope has on your computer. The reason for this is so that your code behaves the same when you submit it to Gradescope as it does when you work on it on your computer. For example, our Gradescope environment uses `numpy` version `1.21.2`; if you install a different version of `numpy` on your computer, for example, you might see different results than Gradescope sees.

How do you install packages, then? `pip` is a common choice, but even though it's widely used, it lacks built-in support for creating isolated environments. This limitation makes it challenging to maintain version consistency and avoid conflicts between packages. **Consequently, we do not recommend relying solely on `pip install` for environment management**, as it may inadvertently introduce incompatible package versions.

`conda`, on the other hand, is a powerful tool that not only installs packages but also manages environments effortlessly. It allows you to create isolated environments and ensures compatibility among the packages within those environments.

**While we coud use `conda`, we'll instead use an even better tool called `mamba`, which is a wrapper around `conda` that is designed to be much faster.** If you should need to install a new Python package, you can use the `mamba` command (after you have `mamba` installed). Inside the terminal, type `mamba install <package_name>`, where `<package_name>` is replaced by the name of the package you want to install, and hit enter. **However, you should only run `mamba install` once you've entered your `dsc80` environment** – more on this below.

---

## Replicating the Gradescope Environment

Below, we're going to walk you through how to create the same environment that Gradescope uses.

### Step 1: Install `mamba`
    
The way to do this depends on whether you're on a Unix-like platform (macOS or Linux) or on Windows.

**Unix-like platforms (macOS or Linux)**:

1. Download the `mamba` installer. To do this, open your terminal and run:


    ```
    curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
    ```

    This will place a file named something like `Miniforge3-Darwin-arm64.sh` wherever you ran the command. If you get an error saying `command not found: curl`, replace `curl -L -O` with `wget` and re-run the same command.

2. Run the installer. To do this, immediately after the last command, run:

    ```
    bash Miniforge3-$(uname)-$(uname -m).sh
    ```

**Windows**:

1. Download the Windows install script from [here](https://github.com/conda-forge/miniforge?tab=readme-ov-file#windows). The file should be named `Miniforge3-Windows-x86_64.exe`.
2. Run the downloaded `.exe` file. Follow the prompts, taking note of the options to "Create start menu shortcut" and "Add Miniforge3 to my PATH environment variable". The latter is not selected by default, but you will want to select it. This allows you to easily run `mamba` commands from from terminals other than the just-installed Miniforge Prompt.
3. From the Start Menu, open the Miniforge Prompt and run:
    ```
    conda init
    ```

### Step 2: Download [`environment.yml`](https://github.com/dsc-courses/dsc80-2026-sp/blob/main/resources/environment.yml)

[This file](https://github.com/dsc-courses/dsc80-2026-sp/blob/main/resources/environment.yml) contains the necessary details to configure your environment. If you take a look at it, you'll see that it contains a specific Python version (`python=3.10`) along with specific package versions (like `pandas==2.2.3` and `requests==2.32.3`, for example).

### Step 3: Create a new `conda` environment

Yes, we said `conda` environment, even though we're using `mamba` to create it.

To create the environment, in your terminal, run:

```
mamba env create -f <path_to_file>
```

Here, `<path_to_file>` should be replaced with a path to the `environment.yml` file you just downloaded, which might be in your Downloads or Desktop folder. For example: `mamba env create -f /Users/yourusername/Desktop/environment.yml`. 

If you get an error saying `environment.yml` does not exist, you probably have the wrong path to the file.

If you get an error saying `mamba` isn't defined, try closing and reopening your terminal first and then rerunning the command.

### Step 4: Activate the environment

To do so, run:

```
mamba activate dsc80
```

If you get an error saying `mamba` isn't defined, try closing and reopening your terminal first and then rerunning the command.

Where did the name `dsc80` come from, you might ask? We defined it for you at the top of `environment.yml` with `name: dsc80`.

---

## Working on Assignments

### Activating the `conda` environment

The setup instructions above only need to be run once. Now, every time you work on DSC 80 assignments, all you need to do is run this command in your terminal:

```
mamba activate dsc80
```

If you need to install any packages into your `dsc80` environment using `mamba install`, make sure to activate the environment first.

If you’re using VSCode, you should select the Python kernel corresponding to the `dsc80` environment to use it.

To open a Jupyter Notebook, use the `jupyter notebook` command in your terminal.

### Using Git

All of our course materials, including your assignments, are hosted on
GitHub in [this Git repository](https://github.com/dsc-courses/dsc80-2026-sp). This means that you'll need to download and use
[Git](https://git-scm.com/) in order to work with the course
materials.

Git is a *version control system*. In short, it is used to keep track of
the history of a project. With Git, you can go back in time to any
previous version of your project, or even work on two different versions
(or \"branches\") in parallel and \"merge\" them together at some point
in the future. We\'ll stick to using the basic features of Git in DSC
80.

There are many graphical user interfaces (GUIs) for working with Git, which you are welcome to use for this class. Janine uses GitHub Desktop. You can also
use the command-line version of Git. To get started, you\'ll need to
\"clone\" the course repository. Navigate to the directory where you want to place your DSC 80 course materials, and run:

    git clone https://github.com/dsc-courses/dsc80-2026-sp

This will copy the repository to the current directory on your computer. You should only need to do this once.

Moving forward, to bring in the latest version of the repository, in your local repository, run:

```
git pull
```

This will **not** overwrite your work. In fact, Git is designed to make it very difficult
to lose work (although it\'s still possible!).

**Merge Conflicts**

You might face issues when using `git pull` regarding merge issues and branches. This is caused by files being updated on your side while we are also changing the [Git repository](https://github.com/dsc-courses/dsc80-2026-sp) by pushing new assignments on our side. Here are some steps you can follow to resolve them:

NOTE: If you're new to working with GitHub pulls, merges, etc., it's a good idea to **save a copy of your important work locally** just in case you accidentally overwrite your files. 

Here are some useful `git` commands to know:

1. `git status` shows the current state of your Git working directory and staging area. It's a good sanity check to start with. You will probably see your project and lab files that you have worked on.
2. `git add .`  will add all your files to be ready to commit.
3. `git commit -m "some message of your choice"`  will commit the files, with some description in the quotations, such as `"progress on questions 1-3 on lab 1". This message can be whatever you want. 

At this stage, if you `git pull`, it should work. You should double-check that you have new files, as well as that your old files are unchanged. If they are changed then you should be able to just copy-paste from your local backup. If this does **not** work then you may have **merge conflicts**, follow the next steps:

4. `git checkout --theirs [FILENAME]`  will tell git that whenever a conflict occurs in `[FILENAME]` to keep your version. Run this for each file with a conflict.
5. `git add [FILENAME]` to mark each file with a conflict as resolved. 
6. `git rebase --continue` or `git merge`, depending on the setup. 


### Choosing a Text Editor or IDE

In this class, you will need to use a combination of editors for doing
your assignments: The Python files should be developed with a text editor (for
syntax highlighting and running doctests) and the data/results should be
analyzed/presented in Jupyter Notebooks. Below is an incomplete list of
IDEs you might want to try. For more information about them, feel free
to ask the course staff.


-   The [JupyterLab](https://jupyterlab.readthedocs.io/en/stable/) text
    editor: Can be used to edit both notebooks and .py files.

-   [VSCode](https://code.visualstudio.com/): Microsoft Visual Studio Code. Ppular and easy to use. Can be used to edit both notebooks and .py files. 

-   [sublime](https://www.sublimetext.com/): A favorite text editor of
    hackers, famous for its multiple cursors. A good, general-purpose
    choice.

-   [atom](https://atom.io/): GitHub's editor. Pretty nice fully
    featured IDE. Can only work locally.

-   [PyCharm (IntelliJ)](https://www.jetbrains.com/pycharm/): For those who
    feel at home coding Java. Can only work locally.

-   [nano](https://www.nano-editor.org/): Available on most unix
    commandlines (e.g. DataHub Terminal). If you use this for more than
    changing a word or two, you\'ll hate your life.

-   [(neo)vim](https://neovim.io/): A lightweight, productive text-editor
    that might be the most efficient way to edit text, if you can ever
    learn how to use it. Justin Eldridge's text editor of choice.

-   [emacs](https://www.gnu.org/software/emacs/): A text editor for
    those who prefer a life of endless toil. Endlessly customizable, it
    promises everything, but you're never good enough to deliver.

### Using VSCode to Run Jupyter Notebooks

Many students like to use VSCode to edit Jupyter Notebooks. If that's you, then you'll need to make sure to activate your `dsc80` conda environment within your notebook in VSCode. Here's how to do that.

1. Open a Juypter Notebook in VSCode.
1. Click "Select Kernel" in the top right corner of the window.
1. Click "Python Environments" in the toolbar that appears in the middle.
1. Select "dsc80 (Python 3.12.12)".
    <center><img src="../assets/images/ts-dsc80-conda.jpg" width=300></center>
