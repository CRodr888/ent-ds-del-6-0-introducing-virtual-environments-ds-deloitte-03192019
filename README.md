
# Introducing Virtual Environments


## Introduction
Up to this point, we have been using libraries that are both very popular and very stable (e.g. Pandas and Beautiful Soup). As you continue to write Python code, you may find yourself using packages that are not so popular (so you may have to install them) or that are changing more quickly (so you will need to have the right version of them installed). In this lesson we'll look at the idea of virtual environments and how they can be used to ensure that you have the right versions of the libraries that you need and that you have the option of packaging up and sharing your environment to make it easier for other people to successfully run the Python scripts you have written.

## Objectives
You will be able to:
* Explain what problems virtual environments solve
* Install a conda virtual environment
* Install new packages using pip

## The Limitations of Libraries

Libraries like Pandas and Beautiful Soup are amazing. They allow us very quickly to create powerful scripts, leveraging a lot of prebuilt functionality. However, they have two limitations. 

### Installation Required

The first is that for your scripts to work, those libraries need to be installed. This is something we haven't come across to date because we've only used very common libraries and they were all included in the distribution of Anaconda that we all installed, but it means that if you start using less popular libraries, every time you share your code with someone else or try to use it on another computer, you may have to install some of the libraries.

### Versioning Issues

Secondly, it is possible that the code that you write needs a particular version of a library. For example, if you were to try some machine learning using TensorFlow and decided to use version 2.0, your code may not work for someone running an older version like 1.10. Of course, all they (or you, if it's you working on another laptop) have to do is to download the latest version. But what happens if you're working on two different projects at the same time? One might depend on features from 1.10 that have been deprecated in 2.0 and the other might require 2.0 to work at all.

In an ideal world, you'd like to be able to jump between the two different versions any time you wanted without having to uninstall and reinstall versions. That's where virtual environments come in.

## Introducing Virtual Environments

With virtual environments you can create multiple "environments" that you can move between just by running a single command. This allows you to easily switch between different setts of libraries, different library versions, and even different versions of Python - you've been using "Python 3", but some people are still using the 2.x versions *(2.5, 2.6, 2.7, etc)*.

There are two common ways to use virtual environments. One is built right into Python. It solves most of the problems we care about and if you want to learn more, feel free to check out [the documentation](https://docs.python.org/3/tutorial/venv.html).

We're going to look at the other common way which is [conda virtual environments](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html). The benefit of conda virtual environments over Python virtual environments is that it allows you to include more than just Python libraries in your virtual environments. So if you needed a particular version of Postgres *(a database server)* or ImageMagik *(a tool for programatically working with images)*, you could include the appropriate versions of those pieces of software in your different virtual environments, even though neither of them are Python libraries. This ends up giving you much more flexibility.

## Installing a Package

Before we get ahead of ourselves and start installing virtual environments, let's learn something simpler - how to install a package.

Let's start with a little test. Run the following cell.


```python
import obscure
```


    ---------------------------------------------------------------------------

    ModuleNotFoundError                       Traceback (most recent call last)

    <ipython-input-1-e7326df84138> in <module>()
    ----> 1 import obscure
    

    ModuleNotFoundError: No module named 'obscure'


Hopefully you got a `ModuleNotFound` error. So, if we want to be able to run that code, we're going to have to install the package. Let's give it a try. There are two ways we could do this - `pip install` or `conda install`. For some packages, some times it's important to pick one over the other (typically you just try one and if it doesn't work, you try the other next!), but most of the time both will work. Let's try the pip install . . .


```python
!pip install obscure
```

    Collecting obscure
      Downloading https://files.pythonhosted.org/packages/92/97/517442fc79453b409e5c1f145f84bf29d96af6b0551812a8027419de1336/obscure-1.0.1-py3-none-any.whl
    [31mdistributed 1.21.8 requires msgpack, which is not installed.[0m
    Installing collected packages: obscure
    Successfully installed obscure-1.0.1
    [33mYou are using pip version 10.0.1, however version 19.0.3 is available.
    You should consider upgrading via the 'pip install --upgrade pip' command.[0m


The `!` allows you to run a shell command (soemthign you'd usually type in a terminal window). When you run that cell, you should see something like this:
    
```
Collecting obscure
Downloading https://files.pythonhosted.org/packages/92/97/517442fc79453b409e5c1f145f84bf29d96af6b0551812a8027419de1336/obscure-1.0.1-py3-none-any.whl
distributed 1.21.8 requires msgpack, which is not installed.
Installing collected packages: obscure
Successfully installed obscure-1.0.1
```

And now we can test whether it worked by trying the import statement again.


```python
import obscure
```

If you run the cell above and don't get any error messages, congratulations - you just installed a library!

## Installing a Virtual Environment

We've created a virtual environment that we use for our career students learning Data Science. Lets go through the process of (a) installing it and (b) "activating" it.

To use a new virtual environment, there are two steps you need to complete. The first step is to create the virtual environment. That may take a few minutes as your computer has to download the necessary version of Python and all of the libraries that you want to be able to use in that environment. The next step then is to “use” the virtual environment by activating it.

Open the Git bash terminal window and navigate to this directory (the instructor will show you how!).

Then to create the environment, type `conda env create -f windows.yml`. Depending on the speed of your computer and your internet connection it may take up to five minutes for this to complete. While it does you should see output similar to that displayed below start to appear in your terminal

![screen-47](http://curriculum-content.s3.amazonaws.com/data-science/screen-47.png)

If you see a message that states “WARNING: A newer version of conda exists”, run `conda update -n base conda` and then try again to create the environment using `conda env create -f windows.yml`.

Next, try activating the environment. Type `source activate learn-env` in the git bash (if you have an issue with running git bash, the command to activate conda within the conda shell on windows is `activate learn-env`).

To confirm that it worked, type `conda info --envs` and confirm that the output in the terminal ends with /learn-env - e.g. * /Users/peterbell/anaconda3/envs/learn-env

Congratulations! You've installed and activated a virtual environment! The one extra thing we need to do is tell Jupyter Notebook to use the virtual environment as well.

## Configuring your Kernel

Jupyter Notebooks run "kernels" - the computational engine used for executing your code. It's important to be running the right kernel within your notebook, otherwise you may get errors stating that you don't have a particular package or have the wrong version of it or even complaints about the version of Python you're running (some packages that work with Python 3.6.6 don't currently support Python 3.7, for example).

It is necessary to run `source activate learn-env` every time you start a new terminal window that you are going to use to run a Jupyter Notebook that should use that conda virtual environment. If you don't do this you will get errors, so please check this first. If you are not sure whether you have activated the environment, in the terminal type `conda list -f obscure` and it should show you that you have v1.0.1 of the "obscure" package. If it doesn't show that, (re)run `source activate learn-env`.

However, there is one more step you need to perform. Firstly you need to ensure your terminal is running the learn-env virtual environment so you have the necessary packages. Then you need to go into your Jupyter Notebook and when viewing a notebook, click on "Kernel" in the top bar, then "Change Kernel" and then pick the learn-env kernel. You must make sure you use the right virtual environment kernel whenever you're working in a Jupyter Notebook if you want the notebook to have access to the packages in the environment.

If for any reason you don't see the learn-env option in the drop down list of kernels, exit the notebook in the browser, close down the notebook server, and in the terminal type `python -m ipykernel install --user --name=learn-env` - that will add the learn-env to your list of kernels and when you restart the Jupyter Notebook server and then open a notebook, you'll be able to select the learn-env option from the list of kernels.

## Summary

In this lesson we provided an introduction to virtual environments so as you start to work with a wider range of libraries you'll be able to ensure that (a) you have the versions of the packages that you need and (b) that other people you might share your scripts with also have the ability to run them successfully. This isn't something you're going to need to use today to complete your capstone project, but it's the kind of thing that will come up one day, and given that this is the last day of class we wanted to make sure to leave you with the tools necessary to handle it!


