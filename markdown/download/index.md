# Downloading Iris

#### <a name="toc"></a> Table of Contents
--------

-   **[Installation Instructions](#install)**
-   **[Run Iris](#run)**
-   **[Update Iris](#update)**
-   **[Troubleshooting][download_trouble]**

-----------------------------------------------------------------------

The Iris software package is available for download through Anaconda. Iris is supported on 64-bit Linux and Macintosh OS X 10.9 - 10.11 computer platforms.

-----------------------------------------------------------------------

### <a name="sysreqs"></a> Iris system requirements

Free disk space:

  * OS X: ~220 MB
  * Linux 64-bit: ~370 MB

## <a name="install"></a> Installation Instructions

These directions assume you are running in a BASH shell. If you are running a C-shell (csh, tcsh), start a BASH shell:

	$ /bin/bash
    
  - If you do not have Anaconda, download Miniconda (a minimal version of Anaconda) for your platform. Otherwise, skip to step 2.

	  * [OS X (64-bit)][conda_osx]
	  * [Linux (64-bit)][conda_l64]
  
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
      
  - Create a conda environment named "iris" with Iris installed in it.

		$ conda create -n iris iris=3.0
	
	Say yes (enter "y") when the download script asks you to "Proceed" in installing the packages.
	    
        ...
        The following packages will be downloaded:
        ...
        
	    Proceed ([y]/n)? y
	    
	    Fetching packages ...
        ....
	    
    
  - Activate the Iris environment
  
        $ source activate iris

  - Run the Iris smoke tests to confirm that Iris was installed successfully:
  
		$ iris smoketest
	
	The terminal output will provide a record of the test and indicate a successful termination or failed attempt. For more details on the Iris smoke test, see the [Iris Smoke Test page][smoke_test].
	
With a successful smoke test run, you're ready to use Iris.
		
## <a name="run"></a> Run Iris

Iris must be run from the conda environment created during installation. It is launched with the command `iris`.

	$ source activate iris    # if you're not already in the iris environment
	$ iris
	     
**IMPORTANT:** If you have set "`iris`" as an alias in your `$HOME/.bashrc` or `$HOME/.bash_profile` to run an older version of Iris, please rename the old alias to something else (for example, "`iris2.0.1`" for Iris v2.0.1). Else, you may launch an older version of Iris.

![Iris GUI](../imgs/iris_desktop_small.png "The Iris Desktop")

**Above:** The Iris Desktop

When you are finished using Iris, you may deactivate the `iris` environment with

	$ source deactivate

|   |
|--:|
|[[Back to Table of Contents][toc]]|

## <a name="update"></a> Update Iris

If you already have Iris installed in a conda environment (Iris v2.1 or higher), you may simply run `conda update iris` in your Iris environment.

    $ source activate iris
    $ conda update iris

This will update your Iris installation to the latest version available.

|   |
|--:|
|[[Back to Table of Contents][toc]]|

<!-- external links-->

[mast]:     		http://mast.stsci.edu/portal/Mashup/Clients/Mast/Portal.html "MAST Portal"
[topcat]:   		http://www.star.bris.ac.uk/~mbt/topcat/ "TOPCAT"
[specview]: 		http://www.stsci.edu/resources/software_hardware/spe%20cview/ "Specview"
[conda_osx]:		https://repo.continuum.io/miniconda/Miniconda2-latest-MacOSX-x86_64.sh "OS X Miniconda"
[conda_l64]:		https://repo.continuum.io/miniconda/Miniconda2-latest-Linux-x86_64.sh "Linux 64 Miniconda"
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
