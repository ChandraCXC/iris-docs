# What's new in Iris?

<table cellspacing="5" cellpadding="5">
      <thead>
      <tr class="newsbar">
        <th align="center" width="10%">Date</th>
        <th align="center">Item</th>
      </tr>
      </thead>



    <tbody>
    
      <tr>
	    <td valign="top">Feb. 22, 2017</td>
        <td valign="top">
          <p>
                <strong>Iris v3.0 Released</strong>
          </p>
          <p>
            Bug fixes and minor updates worked on top of 3.0b2. All website images have been updated for Iris 3.0.
          </p>
      
          <p>
            Please read the <a href="./releasenotes/index.html">Release Notes</a>
            for a full list of bug fixes, enhancements, and caveats.
          </p>
        </td>
	  </tr>
      
      <tr>
	    <td valign="top">Dec. 19, 2016</td>
        <td valign="top">
          <p>
                <strong>Iris v3.0b2 Released</strong>
          </p>
          <p>
            Bug fixes and minor updates worked on top of 3.0b1. Overhaul on user 
            documentation.
          </p>
      
          <p>
            Note that this is a <em>beta</em> release. With the extensive
            rework of Iris's visualization tools, there are a handful of
            capabilities that are currently missing or dissabled as compared to
            Iris 2.1.
          </p>
      
          <p>
            Please read the <a href="./releasenotes/index.html">Release Notes</a>
            for a full list of bug fixes, enhancements, and caveats.
          </p>
	  
        </td>
      </tr>

      <tr>
	    <td valign="top">Aug. 19, 2016</td>
        <td valign="top">
          <p>
                <strong>Iris v3.0b1 Released</strong>
          </p>
          <p>
            Major overhaul of the Visualizer, Metadata Browser, and Fitting Tool.
          </p>
      
          <ul>
            <li>
              New Visualizer which allows click-and-drag panning, a
            fixed viewport, and displays high-resultion (~10<sup>5</sup>
            points) spectra.
            </li>
            <li>
              New Fitting Tool layout. Model functions, parameters, fit
            options, and fit statistics are now displayed in one window.
            </li>
            <li>
              Upgraded to Sherpa 4.8.
            </li>
            <li>
              New Metadata Browser. Users can now invert the selection of
            points. The SED data values (spectral, flux, and error) are
            displayed in the same units as the Visualizer.
            </li>
            <li>
              Updated SED Stacker layout.
            </li>
          </ul>

          <p>
            Note that this is a <em>beta</em> release. With the extensive
            rework of Iris's visualization tools, there are a handful of
            capabilities that are currently missing or dissabled as compared to
            Iris 2.1.
          </p>
      
          <p>
            Please read the <a href="./v3.0b1/releasenotes/index.html">Release Notes</a>
            for a full list of bug fixes, enhancements, and caveats.
          </p>
	  
        </td>
      </tr>
      <tr>
        <td valign="top">May 07, 2015</td>
        <td valign="top">
	  <p>
            <strong>Iris v2.1 Released</strong>
	  </p>
	  
	  <ul>
	    <li>
	      Created SED Stacker, a tool for statistically combining groups of SEDs.
	    </li>
	    <li>
	      Added capability to integrate under fitted model components from
	      the Science Tool.
	    </li>
	    <li>
	      Upgraded to Sherpa 4.7. This allows users to arbitrarily combine
	      template libraries and table models with other libraries, models,
	      and functions in the Model Expression in the Fitting Tool.
	    </li>
	    <li>
	      SEDs can now be saved in ASCII format. The ASCII file may be read
	      directly back into Iris.
	    </li>
	  </ul>
	  
	  <p>
	    Please read the <a href="./v2.1/releasenotes/index.html">Release Notes</a>
	    for a full list of bug fixes and enhancements.
	  </p>
	  
        </td>
      </tr>                      

      <tr>
        <td valign="top">Dec. 03, 2013</td>
        <td valign="top">
	<p>
	  <strong>Iris v2.0.1 Patch Released</strong>
	</p>
        <ul>
          <li>
	    Added tooltips for Fitting Tool models in Preset Components list
	  </li>
          <li>
	    Fixed bug where AB and ST magnitude errors were converted
            incorrectly
	  </li>
          <li>
	    Fixed bug where model parameter results were printed twice
            in text file (from File -&gt; Write to text file)
	  </li>
          <li>
	    Fixed documentation URL displayed when wrong Java version is found 
	  </li>
	</ul>
        <p>
	  Please <strong><a href="download/index.html#download">download the latest
	      release</a></strong> here.
        </p>
        </td>
      </tr>
      <tr>
        <td valign="top">Dec. 03, 2013</td>
        <td valign="top">
	  <p>
	    <strong>CAVEAT:</strong> Supported SED Data Types
	  </p>
          <p>
	    In light of recent helpdesk tickets, we want to fully inform
	    our users that Iris is best suited for broad-band
	    photometric SED analysis. It does provide support for short
	    spectroscopic segments (&lt;~1000 points), but larger segments
	    will take a long time to display and analyze. We are
	    evaluating support for larger spectra in future
	    releases. For more information, please see the <a href="./faqs/index.html">FAQs</a>.
	  </p>
        </td>
      </tr>
    </tbody>
  </table>
