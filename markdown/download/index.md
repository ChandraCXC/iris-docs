# Downloading Iris

#### <a name="toc"></a> Table of Contents
--------

-   **[Quickstart](#quickstart)**
-   **[Detailed Download Instructions](#details)**
    -   [Download and Install Iris](#download)
    -   [Run Iris](#run) 
    -   [Run Smoke Test](#test)
    -   [For C-Shell Users](#cshell)

-----------------------------------------------------------------------

The Iris software package is available for download through Anaconda. Iris is supported on Linux and Macintosh OS X 10.6 - 10.11 computer platforms.

-----------------------------------------------------------------------

### <a name="sysreqs"></a> Iris system requirements

Free disk space:

  * OS X: ~220 MB
  * Linux 64-bit: ~370 MB
  * Linux 32-bit: ~330 MB

Known issues with installing and starting Iris are listed on the [Troubleshooting page][download_trouble].

## <a name="quickstart"></a> Download Iris QuickStart

These instructions tell you how to download and install Iris quickly. For more details, tips-and-tricks and some troubleshooting, read the full direction starting in [Detailed Download Directions](#details).

### Download and Installation Instructions:

These directions assume you are running in a BASH shell. If you are running a C-shell (csh, tcsh), then start a BASH shell:

	$ /bin/bash  # for C-shell users ONLY
    
  - If you do not have Anaconda, download Miniconda (a minimal version of Anaconda) for your platform. Otherwise, skip to step 2.

	  * [OS X (64-bit)][conda_osx]
	  * [Linux 64-bit][conda_l64]
	  * [Linux 32-bit][conda_l32]
  
  - Install Miniconda. Installing Miniconda in batch mode assumes the user agrees with the end user [license agreement][conda_license].

		$ bash Miniconda-latest-Linux-x86_64.sh -b -p $HOME/miniconda
		$ export PATH=$PATH:$HOME/miniconda/bin
      
  - Add `$ export PATH=$PATH:$HOME/miniconda/bin` to your `$HOME/.bashrc` or `$HOME/.bash_profile` so that you can run Anaconda commands from your terminal at any time. For example:

		$ emacs ~/.bashrc
		
		export PATH=$PATH:$HOME/miniconda/bin

    Otherwise, you will need to run `$ export PATH=$PATH:$HOME/miniconda/bin`
    each time before you run Iris.
      
  - Add the CXC and Sherpa conda repositories to your Anaconda configuration:
  
		$ conda config --add channels https://conda.anaconda.org/cxc
		$ conda config --add channels https://conda.anaconda.org/sherpa
      
  - Install Iris. This will create a environment specific to Iris. Say yes (enter "y") when the download script asks you to install the packages.

		$ conda create -n iris iris=3.0

    If you have an environment named `iris` already, you can either rename your
    old environment (with, for example, `mv $HOME/miniconda/envs/iris
    $HOME/miniconda/envs/iris2.1`), give this new Iris installation a new
    enviornment name (with `conda create -n iris30b1 iris=3.0`), or delete
    your old Iris installation entirely (with `rm -rf
    $HOME/miniconda/envs/iris`).
    
  - Start Iris. Activate the Iris environment first. Then, you can run Iris as you would for previous versions.
  
		$ source activate iris
		$ iris
    
    __IMPORTANT:__ If you have set "iris" as an alias in your `$HOME/.bashrc` or `$HOME/.bash_profile` to run an older version of Iris, please rename the old alias to something else (for example, "iris201" for Iris v2.0.1).

  - Run the Iris smoke tests to confirm that Iris was installed successfully:
  
		$ iris smoketest
      
  - When you're finished using Iris, you can restore the original environment:
  
		$ source deactivate
	
For C-shell users: If you wish to run Iris from a C-shell, see the extra steps needed in [For C-Shell Users](#cshell).

|   |
|--:|
|[[Back to Table of Contents][toc]]|

## <a name="details"></a> Detailed Download Directions

### <a name="supported_platforms"></a> Determine if your platform is supported

Iris is supported on Mac OS X 10.6-10.11 64-bit machines and Linux systems.

<!-- 
To see if you Mac is supported, do the following:

  * Choose "About This Mac" from the Apple menu in the upper-left menu bar. You should see the OS X version listed below the Apple icon.
  * Click "More Info".
  * Open the "Hardware" section.
  * Locate the "Processor Name".
![Iris GUI](imgs/download/mac_hardware_overview.png)
  * Compare your Processor Name to information below to determine if your Mac has a 64-bit processor.
![Iris GUI](imgs/download/mac_processor_info.png)
 -->

### <a name="download"></a> Download and Install Iris.

These directions assume you are running in a BASH shell. If you are running a C-shell (csh, tcsh), then start a BASH shell:

    $ /bin/bash  # for C-shell users ONLY
    
  - Iris is now distributed through Anaconda, a Python distribution and package
    manager. If you do not have Anaconda, download Miniconda (a minimal version
    of Anaconda) for your platform. Otherwise, skip to step 2. 
         * [OS X 64-bit][conda_osx]
	 * [Linux 64-bit][conda_l64]
	 * [Linux 32-bit][conda_l32]

  - Anaconda lets you install and manage Python packages without root or administrator permissions. It is also useful for experimenting with different Python versions in isolated environments without fiddling with your system Python distribution. Beyond its use for installing Iris, Anaconda can be a helpful tool to have for other projects. 

  - Install Miniconda. Installing Miniconda in batch mode assumes the user agrees with the end user license agreement found here.
		
		$ bash Miniconda-latest-Linux-x86_64.sh -b -p $HOME/miniconda
		$ export PATH=$PATH:$HOME/miniconda/bin
  - Add `$ export PATH=$PATH:$HOME/miniconda/bin` to your `$HOME/.bashrc` or `$HOME/.bash_profile` so that you can run Anaconda commands from your terminal at any time. Otherwise, you will need to run this line everytime you run Iris. For example, if you've already appended Miniconda to your `PATH`:

        $ echo "export PATH=$PATH" >> ~/.bashrc
      
  - Add the CXC and Sherpa conda repositories to your Anaconda configuration:
  
		$ conda config --add channels https://conda.anaconda.org/cxc
		$ conda config --add channels https://conda.anaconda.org/sherpa
      
  - Install Iris. This will create a environment specific to Iris.

		$ conda create -n iris iris=3.0
      
    You will see something like the following output below. Say yes (enter "y") when the download script asks you to install the packages.

<!-- language: lang-none -->

		Fetching package metadata: ..........
		Solving package specifications: ...............
		Package plan for installation in environment /home/username/miniconda/envs/iris:

		The following packages will be downloaded:

			package                    |            build
			---------------------------|-----------------
			openjdk-8.17.0.3           |                1        63.3 MB
			iris-3.0                   |                3        23.5 MB
			numpy-1.8.2                |           py27_0         7.3 MB
			pyfits-3.3.0               |       np18py27_1         1.9 MB
			python-2.7.12              |                2        13.4 MB
			sampy-1.2.1                |           py27_1          57 KB
			scipy-0.14.0               |       np18py27_0        29.6 MB
			setuptools-25.1.6          |           py27_0         435 KB
			astlib-0.7.0               |       np18py27_2         1.1 MB
			pip-8.1.2                  |           py27_0         1.4 MB
			sherpa-4.8                 |       np18py27_1         6.2 MB
			sedstacker-0.1.0_iris      |       np18py27_3         4.7 MB
			sherpa-samp-3.0            |       np18py27_3          84 KB
			------------------------------------------------------------
												   Total:        90.5 MB

		The following NEW packages will be INSTALLED:

            astlib:      0.7.0-np18py27_1      cxc             
            iris:        3.0-0                 cxc
            numpy:       1.8.2-py27_0                          
            openjdk:     8.17.0.3-1                            
            openssl:     1.0.2k-0                              
            pip:         9.0.1-py27_1                          
            pyfits:      3.3.0-np18py27_1      cxc             
            python:      2.7.13-0                              
            readline:    6.2-2                                 
            sampy:       1.2.1-py27_1          cxc             
            scipy:       0.14.0-np18py27_0                     
            sedstacker:  0.1.0_iris-np18py27_3 cxc             
            setuptools:  27.2.0-py27_0                         
            sherpa:      4.8.0-py27_2          sherpa          
            sherpa-samp: 3.0-np18py27_0        cxc
            sqlite:      3.13.0-0                              
            tk:          8.5.18-0                              
            wheel:       0.29.0-py27_0                         
            zlib:        1.2.8-3
             

		Proceed ([y]/n)? y
		Fetching packages ...
		openjdk-8.17.0 100% |################################| Time: 0:00:07   8.60 MB/s
		iris-3.0-0     100% |################################| Time: 0:00:03   6.62 MB/s
		numpy-1.8.2-py 100% |################################| Time: 0:00:02   3.08 MB/s
		pyfits-3.3.0-n 100% |################################| Time: 0:00:00   6.01 MB/s
		python-2.7.12- 100% |################################| Time: 0:00:35 390.66 kB/s
		sampy-1.2.1-py 100% |################################| Time: 0:00:00   4.51 MB/s
		scipy-0.14.0-n 100% |################################| Time: 0:00:30   1.03 MB/s
		setuptools-25. 100% |################################| Time: 0:00:00   1.67 MB/s
		astlib-0.7.0-n 100% |################################| Time: 0:00:01 695.91 kB/s
		pip-8.1.2-py27 100% |################################| Time: 0:00:01 826.33 kB/s
		sherpa-4.8-np1 100% |################################| Time: 0:00:06 992.10 kB/s
		sedstacker-0.1 100% |################################| Time: 0:00:05 869.50 kB/s
		sherpa-samp-3. 100% |################################| Time: 0:00:00 833.10 kB/s
		Extracting packages ...
		[      COMPLETE    ]|#######################################################################################################| 100%
		Linking packages ...
		[      COMPLETE     ]|#######################################################################################################| 100%
		#
		# To activate this environment, use:
		# $ source activate iris
		#
		# To deactivate this environment, use:
		# $ source deactivate
		#

At this point, Iris is fully installed on your system and ready to be used.

### <a name="run"></a> Run Iris

From the command line, activate the Iris environment. Then, you can run Iris from any directory with the simple command iris.

	$ source activate iris
	$ iris
	     
**IMPORTANT:** If you have set "`iris`" as an alias in your `$HOME/.bashrc` or `$HOME/.bash_profile` to run an older version of Iris, please rename the old alias to something else (for example, "`iris2.0.1`" for Iris v2.0.1).

![Iris GUI](../imgs/iris_desktop_small.png "The Iris Desktop")

**Above:** The Iris Desktop

When you close Iris, you can restore your original environment by entering the following into the command line:

	$ source deactivate
	       
### <a name="test"></a> Run the Iris smoke test

A "smoketest" file is included in the Iris software package to help you verify that Iris has been installed correctly and is working properly on your computer platform.

To run the smoke test, start the Iris environment and run iris smoketest:

	$ source activate iris  # if not already in the environment
	$ iris smoketest
	   
The terminal output will provide a record of the test and indicate a successful termination or failed attempt. For more details on the Iris smoke test, see the [Iris Smoke Test page][smoke_test].

When you're finished using Iris, you can restore the original environment:

	$ source deactivate
	   
### <a name="cshell"></a> For C-shell users

If you wish to run Iris from a C-shell, add the following lines to your $HOME/.cshrc:

	setenv PATH ${PATH}:<path-to>/miniconda/bin   # append the path to miniconda/bin to $PATH
	setenv OLDPATH ${PATH}
	alias source_activate_iris "setenv PATH <path-to>/miniconda/envs/iris/bin:${PATH}"
	alias source_deactivate "setenv PATH $OLDPATH"
	     
where &lt;path-to&gt; is the full path to your Miniconda or Anaconda directory. (**Note:** If you're using Anaconda, replace "`miniconda`" with "`anaconda`")

After sourcing your `$HOME/.cshrc`, you can start Iris with

	% source_activate_iris
	% iris
	     
Once you've closed Iris, you can restore the original environment with

	% source_deactivate
	     
If you want to, you can change the name of "`source_activate_iris`" and "`source_deactivate`" to whatever you'd like, e.g., "`activate_iris`" and "`deactivate`", by editing the aliases listed in your `$HOME/.cshrc`.

If you choose to setup these aliases, whenever you see the following in the Iris documentation:

	% /bin/bash    # C-shell users ONLY
	$ source activate iris
	     
you can skip the `/bin/bash` and replace source activate iris with `source_activate_iris` (or whatever your alias is).

|   |
|--:|
|[[Back to Table of Contents][toc]]|

<!-- external links-->

[mast]:     		http://mast.stsci.edu/portal/Mashup/Clients/Mast/Portal.html "MAST Portal"
[topcat]:   		http://www.star.bris.ac.uk/~mbt/topcat/ "TOPCAT"
[specview]: 		http://www.stsci.edu/resources/software_hardware/spe%20cview/ "Specview"
[conda_osx]:		http://repo.continuum.io/miniconda/Miniconda-3.8.3-MacOSX-x86_64.sh "OS X Miniconda"
[conda_l64]:		http://repo.continuum.io/miniconda/Miniconda-3.8.3-Linux-x86_64.sh "Linux 64 Miniconda"
[conda_l32]:		http://repo.continuum.io/miniconda/Miniconda-3.8.3-Linux-x86.sh "Linux 32 Miniconda"
[conda_license]:	https://docs.continuum.io/anaconda/eula

<!-- threads -->
[sedstacker]: 		../threads/science/sedstacker/index.html "SED Stacker"
[science]: 			../threads/science/index.html "Shift, Interpolate, and Integrate"
[entry]: 			../threads/entry/index.html "Loading SED Data into Iris"
[fit]: 				../threads/fits/index.html "Modeling and Fiting SED Data"
[importer]: 		../threads/importer/index.html "Building and Managing SEDs"
[plot]: 			../threads/plot/index.html "Visualizing SED Data"
[analysis]: 		../threads/analysis/index.html "Analyzing SED Data in Iris"
[save]: 			../threads/save/index.html "Saving SED Data"
[sdk]: 				../threads/sdk/index.html "Developing Plugins: the Iris Software Development Kit"
[plugin_manager]: 	../threads/plugin_manager/index.html "Plugin Manager"

<!-- reference files -->
[download]: 		../download/index.html "Download and Installation"
[smoke_test]: 		../download/smoke_tests.html "Smoke Test"
[macosx105]:		../download/macosx_test.html "Mac OS X 10.5 Download Instructions"
[download_trouble]: ../bugs/smoke.html
[supported_files]: 	../references/importer_files.html
[models]: 			../references/models.html
[faq]: 				../faq/index.html "FAQs"
[releasenotes]: 	../releasenotes/index.html "Release Notes"
[publications]: 	../publications/index.html "Iris Publications"
[bugs]: 			../bugs/index.html "Bugs and Caveats"

<!-- Table of Contents -->
[toc]:      		#toc
