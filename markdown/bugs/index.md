# Iris Bugs & Caveats

[Fitting](#fit) | [Multiple Users](#multiple_users) | [Science Tools](#sci_tools) | [Graphics](#graphics) | [SED Data Types](#sed_data) | [Visualization/Interaction](#visuals)

The following is a list of known limitations of the Iris software. If you encounter a software bug or analysis caveat that is not listed here, please report it to the [CXC Helpdesk][helpdesk].

For troubleshooting the Iris installation, see the [Troubleshooting page][download_trouble].

### <a name="fit"></a> Fitting

#### General Fitting

  * The internal units for fitting in Iris are photons/sec/cm2/angstrom and Angstroms, and so the best-fit parameters values will always be in terms of $photons/s/cm^{2}/Angstrom$ and $Angstroms$, regardless of the user-defined unit settings. 

  * Clicking "Stop" or "Dismiss" while calculating the fit statistics in either the "Fit" or "Confidence" tab may disconnect Sherpa from the SAMP hub. This prevents any more fitting routines within Iris. You can reconnect Sherpa to Iris from the command line:
(in a new Terminal window or tab)

		% /bin/bash       # if in a C-shell
		$ source activate iris
		$ sherpa-samp
  
    Wait 10 seconds for Sherpa to reconnect, then you may continue you fitting session. 

#### Fitting Data with Custom Models

  * When a spectral model component is deleted from the Custom Model Manager, the Sherpa model expression being used for fitting, shown in the Fitting Tool window, is not automatically updated; it needs to be edited manually by the user. 

  * When fitting with a template model, the search method is automatically switched to a grid search over the templates included in the model. The template parameters are interpolated using the default K-nearest neighbor (KNN) algorithm in Sherpa, Iris' fitting engine. 

  * All custom table and template data files must be in ASCII format. Table and template models do not read from FITS files.

  * The data contained in custom table and template models must have the same units that Iris uses internally for modeling and fitting. The x-axis units must be in Angstroms, and the y-axis units should be in photons/s/cm2/Angstrom. (These units match the internal units used for fitting in the original Specview, and which are still used in the Iris components derived from Specview. These components prepare data and model for fitting with Sherpa.)

  * User-definied templates, table models, and functions are not listed by their Component IDs in the Components panel. They are listed as "template," "tablemodel," and "usermodel," respectively, no matter how many user-defined fitting functions are added to the Componets list. For example, if you added two user-defined functions named "modified_blackbody" and "scc," they will appear as "usermodel.m1" and "usermodel.m2" in the Components panel.

### <a name="multiple_users"></a> Multiple Users

  * Iris cannot currently be launched by multiple users on the same system.

### <a name="sci_tools"></a> Science Tools

#### Integration

  * Too few points in the region of interest of the Integrated SED will result in NaNs. In order to obtain good results you need to have a "good" density of points in the interval over which you are integrating. We are not sure how we can define "good." However, problems arise when one interpolates a whole SED with more than 1.5k bins: with too many points the SED Viewer chokes. 

  * All flux calculations, including those calculated from a photometric filter, are recorded as a *flux* quantity, not a flux *density*. The data are converted to erg/s/cm2/Angstrom vs Angstroms for integration. After the integrated fluxes are calculated, the fluxes are recorded in erg/s/cm2 with the effective wavelength as the X-value in Angstroms.
    
    Of course this may not make sense for fluxes calculated through the photometric filters.  If you want to convert these fluxes to flux densities:
    
    1. click the "Save" button in the Flux tab
    2. choose "Angstroms" as the X Units, and "erg/s/cm2" as the Y Units
    3. open the saved text file in a text editor
    4. remove the comments (lines beginning with "#")
    5. load back into Iris, using "Angstroms" as the X axis units, and 
       "erg/s/cm2/Angstrom" as the Y axis units
    
    The points will be loaded in the correct flux density units.

  * Integration under model components: Only one filter/passband can be added to the list for each SED. It is not currently possible to calculate the flux for the same filter with different combinations of model components. This shortcoming of the GUI can be worked around in this way: one can save the results for each component/combination to file, input a different model expression, click calculate, and then save the new results with a different name.

#### SED Stacker 

  * Sometimes the Y-Units for normalizing by Integration may reset to the default unit after switching between Stacks. Please double check that the normalization units are correct before normalizing a Stack.
  
  * After stacking a group of SEDs, the resultant SED is added to the SED Builder. A silent java.lang.NullPointerException exception is raised when a user tries to add new segments to this SED. No warning pops up to the user.

### <a name="graphics"></a> Graphics

  * Some of the Iris windows will not be fully rendered on systems with a very low screen size or screen resolution, in particular netbooks. 

  * OS X users may experience some issues with the internal windows in Iris. Internal Frames misbehave with some versions of Java on OS X. Gray lines may appear around windows after moving or resizing the windows. This does not impact the functionality of Iris, only the appearance. This is most notable on Java 1.8. These lines will disappear if the user focuses another window and clicks back on the original the window.

### <a name="sed_data"></a> SED Data Types

  * Iris is mainly a photometric SED analysis tool, but does provide support for short spectroscopic segments (<~1000 points); larger segments will take a long time to display and analyze. For more info, see the [SED Data Type FAQs entry][faq_sed].

### <a name="visuals"></a> Visualization/Interaction

#### Accessing Metadata

  * Filtering data by filter expressions has been completely redesigned and is much more responsive. However, it only applies to numerical columns. Also, when masking points, a new column is added and column identifiers change. At this time, scientific notation is not fully supported, especially with negative exponents, e.g. 1e-5.

  * Simple scaling ("aperture correction") has been disabled. Future versions of Iris will provide a mechanism for performing arbitrary operations on columns.
  
  * SAMP broadcasting is not available any more from the Metadata Browser directly. One can extract an SED in the Metadata Browser and then use the SED Builder capabilities to broadcast a flattened SED or an arbitrary number of segments.

  * Data can now be sorted only according to one column, not two as in Iris 2.1.

  * It is not currently possible to filter and select data points by selecting them in the Visualizer.

  * The Segment metadata table, both in single-point mode (right click on point) and entire SED mode (Metadata button) also uses some column names taken from that same old Spectrum Data Model. Column names in all-capitals are in fact FITS keywords that are associated to the corresponding utypes in that old Spectrum Data Model. Not all utypes have an associated FITS keyword, so in those cases, the software that builds the table uses as column name the 'name' of the corresponding field in the matadata structure. That may lead to entire sets of metadata to be ignored because these names may not be unique to each type. An example is the column named "Unit" in NED SEDs. There is a field named "Unit" in the Characterization.FluxAxis" element, and another field with same name in the Characterization.SpectralAxis" element. And likely in other places as well. There is no way for the table-building software to tell apart one from the other, once they are taken out of context (that is, striped out from the fully qualified type). Thus the software currently is retaining the last one it finds when traversing the metadata tree. For the interim solution I put in this release for the missing characterization entries, I used in the characterization spatial and time axis columns the fully qualified utype as column name. That is not very practical for the user (the strings are too long), but ensures unambiguous names, and also ensures that every utype gets its own column. 

  * Handling of other elements in the same table, such as SpectralAxis and FluxAxis, is still done by the old FITS/element name mapping. 

#### Missing error bars 

  * Spectral coordinate errors are ignored if present in the input SED data. This means that errors on the X axis are not displayed nor taken into account for modeling.

#### Unexpected changes to data display

  * Residuals and main plot are not bound together when zooming, panning, etc.

  * Depending on the size of the Visualizer window, legend might spill over the bounds of the Visualizer when many segments are displayed. 
    **Workaround:** users can hide the legend from the "View" menu.
  
  * When analyzing SEDs with more than 16 segments, fitting ranges are not visualized in the plotter. However, they are still listed in the Fitting Ranges window.

  * Deleted model components are not removed automatically from the model expression. 

  * Highlighting and deleting multiple models from the Components list simultaneously may result in the deletion of unhighlighted models. Delete models from the Components list one-at-a-time for desirable results. 

|   |
|--:|
|[[Back to top][top]]|

<!-- extra links -->
[faq_sed]:			../faq/sed.html "FAQ SED Data Type"

<!-- threads -->
[sedstacker]: 		../threads/science/sedstacker/index.html "SED Stacker"
[science]: 			../threads/science/index.html "Shift, Interpolate, and Integrate"
[entry]: 			../threads/entry/index.html "Loading SED Data into Iris"
[fit]: 				../threads/fit/index.html "Modeling and Fiting SED Data"
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