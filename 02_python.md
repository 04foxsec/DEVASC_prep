# Introduction to Python

The 200-901 DevNet Associate DEVASC exam is not a Python test per se. You will not be asked to answer esoteric questions about techniques and syntax that only a Python wizard would know. The exam ensures that you are competent enough with Python to know how to interact with Cisco hardware through APIs and to use Cisco software development kits and frameworks such as pyATS and Genie.

Many UNIX-based operating systems, such as Mac and Linux, already have Python installed, but with Windows, you need to install it yourself. This used to be a hassle, but now you can even install Python from the Windows Store. On a Mac, the default version of Python is 2.7, and you should update it to the more current 3.8 version. One of the easiest ways is to head over to python.org and download the latest variant from the source. The installation is fast, and there are many tutorials on the Internet that walk you through the process.

The use of Python 3 has changed dramatically as support for the 2.x version ended in January 2020. The 3.x version came out in 2008 and is the one that you should be using today. Of course, this version issue is still a problem even within the 3.x train of Python and the corresponding modules you may want to use. To address this compatibility conundrum across different versions and modules, Python virtual environments have been created. 
Such an environment allows you to install a specific version of Python and packages to a separate directory structure. This way, you can ensure that the right modules are loaded, and your applications don't break when you upgrade your base Python installation. 

To use virtual environments, you launch Python 3 with the **-m** argument to run the **venv** module. To activate the virtual environment by using the **source** command.

```
#MacOS or Linux
python3 -m venv myvenv
source myvenv/bin/activate
```

```
#Windows
C:\py -3 -m venv myvenv
C:\myvenv\Scripts\activate.bat
```
At this point, you will see your virtual environment name in parentheses at the beginning of your command prompt: ```(myvenv)$```

To turn off the virtual environment, just type **deactivate** at the command prompt, and your normal command prompt returns, indicating that you are using your local system Python setup.

To install new modules for Python, you use **pip**, which pulls modules down from the PyPI repository. ```(myvenv)$ pip install "packagename"```
