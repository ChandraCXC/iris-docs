# Creating Iris Plugins: the Iris Software Development Kit

------------------------------------------------------------------------

## <a name="overview"></a> Overview

#### Synopsis:


Iris plugins are external components that can add functionality to Iris.
For example, the ASDC Data Center, one of the data retrieval engines in
Iris, was a third-party plugin before Iris 2.0. Users may create their
own plugins in Java using the Iris Software Development Kit and Maven, a
tool for building and managing Java projects. This thread explains how
to generate, develop and install Iris plugins. It assumes that the
reader is proficient in Java. Directions for using Maven are provided.

**Last Update:** 24 Mar 2015 : Updated for Iris 2.1 beta. Artifactory is
no longer public, so developers are asked to contact us directly first
before creating a plugin.

## Contact Us for Help

The Iris artifactory from which developers get the Iris Plugin Maven
archetype is not up at the moment. We encourage developers to **contact
us at the [CXC HelpDesk](/helpdesk)** with the tag "Iris" if they wish
to create a plugin.

------------------------------------------------------------------------

## <a name="history"></a> History

| Date          | Change							   |
|---------------|--------------------------------------|
|  10 Oct 2013  | Created. Moved from "How to Create and Install Iris Plugins" to here. |
|  02 Dec 2013  | Updated for Iris 2.0.1 |
|  14 Apr 2014  | Added the [Quick Start](./index.html#quickstart) section. |
|  24 Mar 2015  | Updated for Iris 2.1 beta. Artifactory is no longer public, so developers are asked to contact us directly first before creating a plugin. |


|   |
|--:|
|[[Back to top][top]]|


<!-- external links -->

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