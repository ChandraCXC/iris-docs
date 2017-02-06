# Iris

### VO Spectral Energy Distribution Analysis Tool

[WHAT'S NEW](./news.html) | [WATCH OUT](./bugs/index.html)

------------------------------------------------------------------------

*Iris* is a spectral energy distribution (SED) analysis tool that allows
the astronomer to build, edit, visualize and model SEDs across a broad
spectral range.

<!-- <div style="background:#d8e3ff;margin-left:20px;margin-right:20px"> -->
<div style="margin-left:20px;margin-right:20px; background: #f5f5f5; border-radius: 4px;">

  <div style="margin-left:25px;margin-right:20px">

    <strong>New release: Iris v3.0</strong>
    <p>
    Iris has undergone a round of plastic surgery, with a full overhaul on
    the Visualizer, Metadata Browser, and Fitting Tool. The Visualizer and
    Metadata Browser now use STILTS -- the same library that powers TOPCAT --
    as their backend. High-resoultion spectra can now be plotted. The Fitting 
    Tool encapsulates the models, parameter values, fitting options, and fit 
    statistics in one window. 
    </p>
    <p>
    The changes to Iris 3.0 are mostly user-interface updates and bug
    fixes. The algorithms behind building, editing, and fitting SEDs remains
    the same unless otherwise noted.
    </p>
    <p>
    For a full list of the changes introduced in Iris 3.0, please see 
    the <a href="./releasenotes/index.html">Release Notes</a>.
    <strong><a href="./download/index.html">Download Iris v3.0</a></strong>.
    </p>
  </div>

</div>

<div align="center">

<img src="./imgs/new_homepage_pic.png" 
     href="./intro/index.html" 
     alt="Iris desktop application"/>

</div>

*Iris* is a Virtual Observatory downloadable application for analysis of
1-D astronomical spectral energy distributions (SEDs). Iris allows the
astronomer to build a SED of a source from multiple, separate data
segments or photometric points, gathered from various observatories
across a wide spectral range, and fit the aggregate SED with emission
and/or absorption spectral models; individual data segments may also be
separately analyzed. SED data may be uploaded into the application from
IVOA-compliant VOTable and FITS format files, or imported directly from
the NASA Extragalactic Database and Italian Space Agency Science Data
Center (ASDC); data written in non-native formats may be converted using
the SED Builder portion of the tool. Iris can save SED data files in one
of the aforementioned supported file formats, as well as files for
restoring custom fitting sessions.

*Iris* seamlessly combines key features of several existing astronomical
software applications to streamline and enhance the SED analysis
process; *Sherpa* for spectral model fitting, and the NASA Extragalactic
Database (NED) and Italian Space Agency Data Center (ASDC) for data access. We
strongly encourage you to provide feedback on your experience with the tool by
sending your comments, suggestions, and questions to the [**CXC
HelpDesk**](/helpdesk). 

------------------------------------------------------------------------

### Citing *Iris* in a Publication

**If you are writing a paper and wish to cite *Iris*, we recommend the
following papers and presentations:**

 [Iris: An Extensible Application for Building and Analyzing Spectral Energy Distributions](http://arxiv.org/abs/1407.6916) [**\[PDF\]**](files/aciris.pdf) 
:   Laurino, Omar; Budynkiewicz, Jamie; D'Abrusco, Raffaele;
    Bonaventura, N.; Busko, I.; Cresitello-Dittmar, M.; Doe, S.; Ebert,
    R.; Evans, J.; Norris, P.; Pevunova, O.; Refsdal, B.; Thomas, B.;
    Thompson, R., 2014, Astronomy & Computing,
    DOI: 10.1016/j.ascom.2014.07.004.

 [Iris: The VAO SED Application](http://adsabs.harvard.edu/abs/2012ASPC..461..893D) [**\[PDF\]**](./publications/files/sdoe_vao.pdf) 
:   Doe, Stephen; Bonaventura, N.; Busko, I.; D'Abrusco, R.;
    Cresitello-Dittmar, M.; Ebert, R.; Evans, J.; Laurino, O.; McDowell,
    J.; Pevunova, O.; Refsdal, B., 2012, ADASS XXI, ASP Conference
    Series, 461, 893.

 [Constructing and Analyzing Spectral Energy Distributions with the Virtual Observatory](http://adsabs.harvard.edu/abs/2013AAS...22124038L) [**\[PDF\]**](./publications/files/IrisScience.pdf) 
:   Laurino, Omar; Busko, I.; Cresitello-Dittmar, M.; D'Abrusco, R.;
    Doe, S.; Evans, J.; Pevunova, O.; Norris, P., AAS Meeting \#221,
    \#240.38, Jan 2013.

 [Extending Iris: The VAO SED Analysis Tool](http://adsabs.harvard.edu/abs/2013ASPC..475..295L) **[\[PDF\]](./publications/files/P020.pdf) | [\[PDF (poster)\]](./publications/files/IrisUrbanaADASS.pdf)** 
:   Laurino, O.; Busko, I.; Cresitello-Dittmar, M.; D'Abrusco, R.; Doe,
    S; Evans, J. D.; Pevunova, O., 2013, ADASS XXII, ASP, 475, 295.


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