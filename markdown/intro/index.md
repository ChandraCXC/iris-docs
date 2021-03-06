# About Iris

Iris is a downloadable Graphical User Interface (GUI) application which allows the astronomer to build and analyze wide-band Spectral Energy Distributions (SEDs). SED data may be loaded into Iris from a file on the user's local disk, from a remote URL, or imported directly from the NASA Extragalactic Database (NED) for analysis.

<!-- TODO: wrap in some color. Make it stand out. -->
***Need help? Have any questions or comments about Iris? Contact us at the [CXC HelpDesk][helpdesk].*** We welcome any feedback, and are happy to help you out. Please select "Iris" from the list of dropdown categories, and we will get back to you within 24 hours.


[![Iris screenshot image](./imgs/about-image_small.png)](./imgs/about-image.png)

The components of Iris have been contributed by members of the [Virtual Astronomical Observatory][vao] (VAO). Sherpa, contributed by the Chandra project at the Smithsonian Astrophysical Observatory (SAO), provides a library of models, fit statistics, and optimization methods for analyzing SEDs; the underlying i/o library (SEDlib), also contributed by SAO, is written to the [IVOA Spectrum Data Model 1.03 standard][specdm]. NED is a service provided by IPAC at Caltech for easy location of the data available for a given extragalactic astronomical source, including SEDs. The ASI Science Data Center (ASDC) also provides a plugin to their database, where the user can retrieive photometric data within a search radius and time period. The SED Builder which is bundled with Iris, and contributed by SAO, is a tool for converting non-standard SED data files into a format supported by Iris, so that the file output by the tool may be loaded into Iris for analysis. As of Iris 3.0b1, data visualization -- plotting and tabular manipulation capabilities -- is also contributed by SAO, and is built using the [STILTS][stilts] library. 

Communication between Iris tools and Sherpa is managed by a Simple Application Messaging Protocol (SAMP) connection. Iris packages SED data, model definitions and starting parameter values, and sends them to Sherpa whenever a fit to a SED is done. The goal is to seamlessly combine the power of already-built astronomy packages and services into one environment, without reinventing the wheel. We have named this combined software package "*Iris*".

Bugs and caveats associated with this release of the Iris software are documented on the [Bugs & Caveats][bugs] page.

Iris is funded by and actively developed at the [Chandra X-Ray Observatory][cxc] (CXC) at [SAO][sao]. Iris was originally developed by the [VAO][vao] from 2011 to 2014 .

|   |
|--:|
|[[Back to top][top]]|


<!-- external links -->
[specdm]: http://www.ivoa.net/Documents/REC/DM/SpectrumDM-20071029.html "IVOA Spectrum Data Model"
[vao]: http://usvao.org "Virtual Astronomical Observatory"
[sao]: http://cfa.harvard.edu/sao "Smithsonian Astrophysical Observatory"
[stilts]: http://www.star.bris.ac.uk/~mbt/stilts/ "Starlink Tables Infrastructure Library Tool Set"

<!-- threads -->
[sedstacker]: 		../../threads/science/sedstacker/index.html "SED Stacker"
[science]: 			../../threads/science/index.html "Shift, Interpolate, and Integrate"
[entry]: 			../../threads/entry/index.html "Loading SED Data into Iris"
[fit]: 				../../threads/fit/index.html "Modeling and Fiting SED Data"
[importer]: 		../../threads/importer/index.html "Building and Managing SEDs"
[plot]: 			../../threads/plot/index.html "Visualizing SED Data"
[analysis]: 		../../threads/analysis/index.html "Analyzing SED Data in Iris"
[save]: 			../../threads/save/index.html "Saving SED Data"
[sdk]: 				../../threads/sdk/index.html "Developing Plugins: the Iris Software Development Kit"
[plugin_manager]: 	../../threads/plugin_manager/index.html "Plugin Manager"

<!-- extras (Iris models) -->
[brokenpowerlaw]:   ../../references/models.html#brokenpowerlaw "brokenpowerlaw"
[blackbody]:		../../references/models.html#blackbody "blackbody"

<!-- reference files -->
[download]: 		../../download/index.html "Download and Installation"
[smoke_test]: 		../../download/smoke_tests.html "Smoke Test"
[macosx105]:		../../download/macosx_test.html "Mac OS X 10.5 Download Instructions"
[download_trouble]: ../../bugs/smoke.html
[supported_files]: 	../../references/importer_files.html
[models]: 			../../references/models.html
[faq]: 				../../faq/index.html "FAQs"
[releasenotes]: 	../../releasenotes/index.html "Release Notes"
[publications]: 	../../publications/index.html "Iris Publications"
[bugs]: 			../../bugs/index.html "Bugs and Caveats"

<!-- CXC links -->
[helpdesk]:			/helpdesk/ "CXC HelpDesk"
[sao]:				http://cfa.harvard.edu/sao "Smithsonian Astrophysical Observatory"
[cxc]:				/ "Chandra X-Ray Observatory"
[sherpa]:			/sherpa/ "Sherpa"

<!-- Navigation -->
[toc]:				#toc
[top]:      		#top