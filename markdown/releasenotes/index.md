# Iris Release Notes

## Iris 3.0 Release Notes

Iris 3.0b1 introduced a new infrastructure for visualizing and fitting
spectrophotometric data. The new infrastructure allows users to load and fit
high resolution spectra as well as broadband, multi-wavelength
spectrophotometric datasets. The new infrastructure is also more flexible and
it will enable future extensions of the Iris functionality. Moreover, Iris 3.0b1
introduces a simple client for the Vizier/CDS SED service while keeping the
dedicated clients to NED and ASDC services. This release also fixes several bugs
and introduces some new functionality and user interface improvements, as
specified in more detail below, component by component.

3.0b2 was a much smaller addition of bug fixes and a few minor enhancements to the 3.0b1 release. 

Iris 3.0 introduced a complete update of the user documentation, along with a handful of remaining bugs fixes.

The release notes shown here are a combination of the 3.0 releases.

### Fitting Tool

The fitting tool GUI has been completely redesigned. It now relies on a single
window, and information should be easier to set and retrieve.

  * The list of available models is always visible: you can double-click on a model to make it part of your model expression.
  * A search box allows to easily filter the model components, and a description box displays simple documentation for the model.
  * We introduced a simple "Chi2" statistic (In Iris 2.1 you had to select one of the specialized chi2 statistics and Sherpa would fall back to Chi2 if errors were provided by the user).
  * Model parameter values are updated on the fly.
  * You can select ranges by either clicking on the plot or by manually setting ranges in any units.
  * Model components now have unique IDs in a working session. Component IDs do not change if components are deleted.
  * Model expressions are validated on the fly, so you know if a model expression is not valid as soon as you type it.
  * Output files created by the "Save Text" option now contain more information, including the location of custom user models.
  * Models can be saved as Json files and then loaded back into Iris. Note that the Iris 1 and 2 xml serializations are not supported any more. If you have such a file and you want it converted to the new format, please let us know.
  * Models can be evaluated even if they have not been fitted. So for instance you can change model parameters and re-evaluate the model, or evaluate individual model components.
  * You can right-click on a model component to select it and remove it from the expression.

### SED Viewer

The viewer component was completely redesigned. It now relies on STILTS as a
plotting backend. Functionality is mostly unchanged, but now you can:

  * plot and analyze high resolution spectra.
  * coplot SEDs with their models.
  * plot model functions even if they have not been fitted. You can also plot
individual model components.

Note that SED with multiple segments show points belonging to different
segments with different colors. The current palette has 16 distinct colors.
More than 16 segments would result in points having color differences that are
hardly noticeable, not to mention a rather long legend. When more than 16
segments are plotted, Iris will show the SED as a single segment.
The Metadata Browser is unaffected by the number of segments.

### Metadata Browser

The metadata browser GUI, which is accessible by clicking "Metadata" on the
Visualizer toolbar, has been completely redesigned. Functionality is mostly
unchanged, however:

  * Points can now be masked and unmasked directly from the metadata browser.
  * Masked points are not included in the fit.

### Sed Stacker

  * The GUI was redesigned to follow suggestions from users. The SED Stacker frame
is now laid out in a horizontal fashion, so users will move from left to right
on the frame as they work on a Stack. Open Stacks and Stack Management are on
the left; a list of added SEDs (with Add/Remove capabilities) is in the center;
redshifting, normalizing, and stacking options are on the far right.
  * Right-clicking a Stack in the Open Stacks window now offers a Remove option.
  * We also fixed some typos in the GUI.

-----------------------

## Caveats and Known Bugs

The following is a list of caveats and bugs that were documented this
release. For the complete report of caveats and known bugs, please view the
list in [Bugs & Caveats][bugs]. If you experience any other issues with Iris,
please send us a message at the [CXC HelpDesk][helpdesk].

### Visualizer

  * Residuals and main plot are not bound together when zooming, panning, etc.
  * Depending on the size of the Visualizer window, legend might spill over
    the bounds of the Visualizer when many segments are displayed.
    **Workaround:** users can hide the legend from the "View" menu.
  * It is not possible to filter data points by selecting them
    in the Visualizer.
  * When analyzing SEDs with more than 16 segments, fitting ranges are not
    visualized in the plotter. However, they are still listed in the
    Fitting Ranges window.

### Metadata Browser

  * Filtering data by filter expressions has been completely redesigned and is much more responsive. However, it only applies to numerical columns. Also, when masking points, a new column is added and column identifiers change. At this time, scientific notation is not fully supported, especially with negative exponents, e.g. 1e-5.
  * Simple scaling ("aperture correction") has been disabled. Future versions of Iris will provide a mechanism for performing arbitrary operations on columns.
  * SAMP broadcasting is not available any more from the Metadata Browser directly. One can extract an SED in the Metadata Browser and then use the SED Builder capabilities to broadcast a flattened SED or an arbitrary number of segments.
  * Data can now be sorted only according to one column, not two as in Iris 2.1.

### Sed Stacker

  * After stacking a group of SEDs, the resultant SED is added to the SED Builder. A silent java.lang.NullPointerException exception is raised when a user tries to add new segments to this SED. No warning pops up to the user.
  * Sometimes the normalization configuration parameters don't update correctly when you switch between Stacks.

-------------------------

<!--
The following bugs and caveats will be addressed before the Iris 2.1 release.

  * In SED Stacker, sometimes the Y-Units for normalizing by Integration may reset to the default unit after switching between Stacks.
-->

## Previous Release Notes

  * [v3.0b2](/iris/v3.0b2/releasenotes/index.html)
  * [v2.1](/iris/v2.1/releasenotes/index.html)
  * [v2.0.1](/iris/v2.0.1/releasenotes/index.html)
  * [v2.0](/iris/v2.0/releasenotes/index.html)
  * [v1.2](/iris/v1.2/releasenotes/index.html)
  * [v1.1](/iris/v1.1/releasenotes/index.html)
  * [v1.0](/iris/v1.0/releasenotes/index.html)
  

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
