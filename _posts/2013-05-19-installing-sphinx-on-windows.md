---
layout: post
title: Installing Sphinx on Windows
date: 2013-05-19 12:41
author: kal
comments: true
categories: [.NET Development, General]
---
<a href="http://sphinx-doc.org/">Sphinx</a> is an open-source tool for creating documentation. Written originally for the documentation of Python projects it also supports C/C++ with plans in the pipeline for support of other languages. Right now, my interest in Sphinx is that it is the tool used by <a href="https://readthedocs.org/">readthedocs.org</a> where I am planning to host the documentation for <a href="http://brightstardb.com/">BrightstarDB</a>.

BrightstarDB is a .NET application written in C# and I'm quite happy with the output of <a href="http://shfb.codeplex.com/">Sandcastle</a> for the API documentation. However the developer and user docs were all originally created using the (commercial) <a href="http://www.helpandmanual.com/">Help &amp; Manual</a> application - which is a great documentation tool in its own right but would require contributors to the project to purchase a license in order to update or extend the docs.

Getting a local version of Sphinx running is the first step in evaluating if this approach is going to be feasible and as I'm developing on Windows 8, getting it running under Windows is my priority. So my goal here is to document how to install all you need to run Sphinx on Windows - with the qualifier that I'm doing this on Windows 8. YMMV on other Windows OSes.
<ol>
	<li><strong>Install Python 2.7</strong>: At the time of writing Python 2.7.5 is the latest Python 2 release. The Python project has Windows installers available at <a href="http://www.python.org/download/">http://www.python.org/download/</a>. As my OS is 64-bit, I used the "Python 2.7.5 Windows X86-64 Installer".</li>
	<li><strong>Add the Python directory to your path</strong>: By default Python will install in C:\Python27 but will not add itself to your PATH environment variable. I find it useful to do that so I don't have to keep typing the full path to the python.exe that you use to run Python scripts.</li>
	<li><strong>Install setuptools</strong>: The current version is 0.6c11 and you can get it from <a href="https://pypi.python.org/pypi/setuptools">https://pypi.python.org/pypi/setuptools</a> Installation instructions for Windows are on that page and differ for 32-bit vs 64-bit OS. The basic procedure is to download <a href="http://peak.telecommunity.com/dist/ez_setup.py">easy_setup.py</a> and then run it. If you updated the PATH environment variable as suggested above, then this is as simple as opening a new command prompt, cd to the directory you downloaded easy_setup.py to and typing:
<pre>python ez_setup.py</pre>
You will see output from the script as it downloads and installs setuptools into your Python directory.</li>
	<li><strong>Add the Python scripts directory to your PATH</strong>: The core setuptools scripts get installed under {Python Directory}\Scripts and the Sphinx scripts will get installed in the same location so it is sensible to add this directory to your PATH environment variable. If you went for the default installation location you will add C:\Python27\Scripts to your PATH.</li>
	<li><strong>Download the Sphinx egg</strong>: Eggs are Python packages that make it easier to distribute and install Python applications. The Sphinx egg can be found at <a href="https://pypi.python.org/pypi/Sphinx">https://pypi.python.org/pypi/Sphinx</a>. At the time of writing the version is 1.2b1.</li>
	<li><strong>Install the Sphinx egg</strong>: Open a new command prompt (to get your updated PATH) and cd to the directory you downloaded the .egg file to. You can then use setuptools to install the egg like this:
<pre>easy_install Sphinx-1.2b1-py2.7.egg</pre>
The package will install the Sphinx scripts and download and install a set of dependencies. The installation process produces a number of warning messages about not finding files but the installation runs through to completion OK.</li>
	<li><strong>Try a Sphinx "Hello World"</strong>: The Sphinx project have <a href="http://sphinx-doc.org/tutorial.html">a more thorough tutorial.</a> But in a nutshell this is what to do (assuming you are still in the same command prompt window) - the following assumes you have your Python directory and Python Scripts directory included in your PATH environment variable.
<ol>
	<li><strong>Initialise your project</strong>. The following command create and initialize a directory that will contain your documentation:
<pre>mkdir MyFirstDoc
cd MyFirstDoc
sphinx-quickstart</pre>
There now follows a list of questions. Apart from the project name, author and release number, the questions have default answers which for this quick runthrough you can just accept by pressing enter.</li>
	<li><strong>Edit index.rst</strong>. The initialization process creates a starter file (by default it will be called index.rst). You will want to keep the toctree directive, but you can add more content before or after it. The <a href="http://sphinx-doc.org/rest.html#rst-primer">reStructuredText Primer</a> on the Sphinx project site guides you through the basic constructs that are pretty simple to get the hang of.</li>
	<li><strong>Make the docs</strong>. The initialization process for Sphinx has helpfully added a make.bat file to your documentation directory so the only command you need to produce your documentation in HTML is:
<pre>make html</pre>
</li>
	<li><strong>View your work</strong>: You should now be able to view the glorious generated HTML by typing:
<pre>_build\html\index.html</pre>
</li>
</ol>
</li>
</ol>
And that's all there is to it - should take you about 10 or 15 minutes from start to end. Of course, now the hardest part, I have to start writing the docs...

