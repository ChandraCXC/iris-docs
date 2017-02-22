# Installation Troubleshooting

The following is a list of known issues that may arise while installing or attempting to run Iris. If you encounter a problem that is not listed here, first check for it on the [Iris Bugs & Caveats page][bugs], and then contact the [CXC Helpdesk][helpdesk] for assistance, if necessary. It is recommended that you include in your bug report the results of the [Iris installation smoke test][smoke].

-----------------------

[I exited Iris with a Force Quit or 'kill' command; now, it does not run properly.](#forcequit)

[(OS X) Smoke tests fail with "Error: Sherpa didn't respond to ping."](#libgcc_missing)

-----------------------

### <a name="forcequit"></a>I exited Iris with a Force Quit or 'kill' command; now it does not run properly.

If the Iris application is killed off either by Force Quit (on Linux or Mac) or the 'kill' command, as opposed to the Iris "File -> Exit" menu option, the Sherpa program may survive as a spurious Python process. As a result, the next time you try to use Iris, it may not work properly. To remedy the problem, you can end the spurious process using 'ps' and 'kill' or using System Monitor. The process name should appear as something like 'python2.7'.

This occurs because Iris is responsible for starting and stopping the Sherpa Python process. If Iris is killed without executing its usual shutdown procedure, Sherpa could be left running. Since Iris uses SAMP to communicate, the spurious Sherpa process can conflict with Iris when it tries to establish a new connection.

You can also confirm the issue by inspecting the Iris log file located in your home directory, `$HOME/.vao/iris/log.txt` (or wherever your `$IRIS_LOG_LOCATION` points too), which should contain an error message indicating the problem.

### <a name="libgcc_missing"></a>Smoke tests fail with "Error: Sherpa didn't respond to ping"

If you get this error, first try running the smoke tests with a longer timeout period, as we do below:

	% iris smoketest 30
       
This should allow enough time for Sherpa to respond to the ping, and for the test to pass.

If the tests still fail, check to see if you have `/usr/local/lib/libgcc_s.1.dylib` on your system:

	% ls /usr/local/lib/libgcc_s.1.dylib
       
If the file doesn't exist, (if it returns something like "`ls: cannot access /usr/local/lib/libgcc_s.1.dylib: No such file or directory`"), then search for your system's `libgcc\_s.1.dylib` library, create a softlink to this directory, and rerun the smoketests:

	% python -c "import time; print time.__file__"

	/anaconda/lib/python2.7/lib-dynload/time.so              # Your result may vary

	% otool -L /anaconda/lib/python2.7/lib-dynload/time.so   # Take your result from above and run 'otool -L <result>'

	/anaconda/lib/python2.7/lib-dynload/time.so:
	/usr/lib/libgcc_s.1.dylib (compatibility version 1.0.0, current version 1.0.0) # create softlink to this file
	/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 111.0.0)

	% sudo ln -s /usr/lib/libgcc_s.1.dylib /usr/local/lib/libgcc_s.1.dylib
       
This will ask you for your password. Type it in when it asks.

If you don't have a `/usr/local/lib directory`, make it:

	% sudo mkdir /usr/local/lib
       
Then try creating the softlink, and rerunning the smoketests.

If you're still having issues, please contact us at the [CXC HelpDesk][helpdesk] with the tag "Iris."

|   |
|--:|
|[[Back to top][top]]|

<!-- external links-->

[oracle]:			http://www.oracle.com/technetwork/java/javase/index-137561.html "Oracle"
[mast]:     		http://mast.stsci.edu/portal/Mashup/Clients/Mast/Portal.html "MAST Portal"
[topcat]:   		http://www.star.bris.ac.uk/~mbt/topcat/ "TOPCAT"
[specview]: 		http://www.stsci.edu/resources/software_hardware/spe%20cview/ "Specview"
[conda_osx]:		http://repo.continuum.io/miniconda/Miniconda-3.8.3-MacOSX-x86_64.sh "OS X Miniconda"
[conda_l64]:		http://repo.continuum.io/miniconda/Miniconda-3.8.3-Linux-x86_64.sh "Linux 64 Miniconda"
[conda_l32]:		http://repo.continuum.io/miniconda/Miniconda-3.8.3-Linux-x86.sh "Linux 32 Miniconda"

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

<!-- CXC links -->
[helpdesk]:			/helpdesk/ "CXC HelpDesk"
[sao]:				http://cfa.harvard.edu/sao "Smithsonian Astrophysical Observatory"
[cxc]:				/ "Chandra X-Ray Observatory"
[sherpa]:			/sherpa/ "Sherpa"

<!-- Navigation -->
[toc]:				#toc
[top]:      		#top
