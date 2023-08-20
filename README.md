This is Python version 2.7.11, modified to build with Visual Studio 2015 Update 3.
==================================================================================

Copyright (c) 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011,
2012, 2013, 2014, 2015 Python Software Foundation.  All rights reserved.

Copyright (c) 2000 BeOpen.com.
All rights reserved.

Copyright (c) 1995-2001 Corporation for National Research Initiatives.
All rights reserved.

Copyright (c) 1991-1995 Stichting Mathematisch Centrum.
All rights reserved.

Why?
----

If you HAVE to work with older maya versions, (from 2018 to 2022 in Python 2
mode) you are stuck with python 2.7.11 even though it has been deprecated for
a while. To make matters worse, the python interpreter in Maya has been 
compiled with Visual Studio 2015 Update 3 (_MSC_VER 1900). This means that any
of the python packages with binary extensions still available on PyPi for 2.7 
are unusable as they were compiled with Visual Studio 2008 (_MSC_VER 1500).

Due to Maya basing the python interpreter on the embedded package (with the 
stdlib zipped up), and having a non standard layout, tools like virtualenv
also do no work correctly.

In order not to let this now archaic setup prevent me from using the wider
python ecosystem in an internal pipeline I'm determined to drag it kicking 
and screaming into the modern world. This is the first piece of that endeavour.

Goal
----

If you compile any python packages against this build of python, they will load
fine in Maya 2018 until Maya 2022 with Python 2. It will have the latest
compatible version of the following packages pre-installed:

| Package    | Version |
| ---------- | ------- |
| pip        | 20.3.4  |
| setuptools | 44.1.1  |
| wheel      | 0.37.1  |
| virtualenv | 20.15.1 |

You can now create a virtualenv with your desired packages, and add the 
resulting site-packages folder to the PYTHONPATH environment variable
before launching maya to make them available there too!

This build should not be used for anything else, and I will only consider
fixing bugs or issues if they interfere with that goal.

Success Criteria
----------------

Analysing the documention and comparing the python embedded in Maya gives with
the official 2.7.11 installer gives us the following differences:

 - Build with Visual Studio 2015 - Update 3
 - Build against Windows 10 SDK (10.0.10586.0)
 - Using OpenSSL 1.0.2h
 - Using sqlite 3.6.21
 - TKinter is not available, so need to worry about tcl/tk.

 If you extract the Python27.zip stdlib shipped with Maya, it will contain a
 `test` folder which is the python testsuite. I want the results of running the
 testsuite on this build and in maya to be as identical as possible.

Requirements
------------

Building this repository requires the following:

 - A python interpreter >= 3.6
 - Install svn from https://sliksvn.com/pub/Slik-Subversion-1.14.2b-x64.zip.
 - Install Visual Studio 2015 Community (Update 3) from
   https://download.microsoft.com/download/b/e/d/bedddfc4-55f4-4748-90a8-ffe38a40e89f/vs2015.3.com_enu.iso
   In the installer I deselected everything, and then added everything under
   `Programming Languages | Visual C++` as well as `Windows and Web Development |
   Universal Windows App Development Tools | Windows 10 SDK (10.0.10586.0)`
   which is the SDK Maya is built with.

Development Log
---------------

 - Forked cpython, created a new branch called vs2015-x64, and pushed it 
   to the repository.
 - Forked cpython-source-deps in case any dependencies need patched
 - Added a README.md with an explanation of why this madness exists.

License information
-------------------

See the file "LICENSE" for information on the history of this
software, terms & conditions for usage, and a DISCLAIMER OF ALL
WARRANTIES.

This Python distribution contains no GNU General Public Licensed
(GPLed) code so it may be used in proprietary projects just like prior
Python distributions.  There are interfaces to some GNU code but these
are entirely optional.

All trademarks referenced herein are property of their respective
holders.
