# Configuring snappy and doing things with it

snappy is the Python library that does all the things one would normally do with the software SNAP of ESA, such as processing satellite products from the Sentinel platforms.

BE AWARE
This repository is for personal use and thus has a number of constraints that come from the fact that I have a certain machine and a fairly limited knowledge of coding. Any advice is welcome. That said, what I am working with is:
- Windows 10, 64bit
- SNAP 8.0 Desktop 64 bit
- Visual Studio 2019 Community, or Visual Studio 16.9.4
- Python 3.8 64bit
- Apache Maven 3.8.1
- Java 16.0.1


## Cookbook
You will need some ingredients for configuring snappy correctly.
- a SNAP build: I am working with the latest version (8.0), installed on my computer: get it from https://step.esa.int/main/download/snap-download/
- Visual Studio with Visual Studio C++: get it from https://visualstudio.microsoft.com/it/downloads/
- a python interpreter: from what I understood, snappy should work only with 2.7, 3.4 and 3.6 releases, but it is working fine with my 3.8. Just so you know. https://www.python.org/downloads/release/python-380/
- you need Java! https://www.java.com/en/download/ie_manual.jsp
- you need Maven! https://maven.apache.org/download.cgi
- you also need to build a jpy wheel to let Java talk properly with Python: you can do it by downloading the whole folder at https://github.com/bcdev/jpy.git and then following the steps below

These are the main ingredients.
- if you already had SNAP BUT you didn't configure it for python usage during installation, you can do it by following the steps at https://senbox.atlassian.net/wiki/spaces/SNAP/pages/50855941/Configure+Python+to+use+the+SNAP-Python+snappy+interface; otherwise, when installing properly let it know that you want a bridge with Python by selecting your interpreter in the dedicated step of the installation;
- after downloading the zip folder for the jpy wheel, unzip it and copy paste into your snappy directory: you should find it in C:\Users\*\.snap\snap-python\snappy

Now the part about environment variables: you need a lot of new variables and they must be set properly for everything to work.
Go into System -> System Properties -> Advanced -> Environment variables
Then set or create new:
- into user variables:
  - var: M2         value: *\apache-maven-<version>\apache-maven-<version>\bin
  - var: M2_HOME    value: *\apache-maven-<version>\apache-maven-<version>
  - var: JAVA_HOME  value: *\Java\jdk-16.0.1\
  - var: VS100COMNTOOLS   value: *\Microsoft Visual Studio\2019\Community\Common7\Tools
- into system variables:
  - var: PATH       add values: *\Python<version>\, *\apache-maven-<version>\apache-maven-<version>\bin

Then open a command line in the bin folder of the SNAP installation directory. Run

$ snappy-conf <python-exe>

where the path to python.exe is the full path. This should work.

To make snappy accessible everywhere, do the following:
$ cd <snappy-dir>/snappy
$ <python-exe> setup.py install
  
That's it! I guess! Still working on this repository.
