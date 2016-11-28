# Modeling and Fitting SED Data in Iris

------------------------------------------------------------------------

## <a name="overview"></a>Overview

#### Synopsis:

Astronomers analyze spectral energy distributions (SEDs) by fitting them
with models over a wide range in wavelength, from gamma rays to radio
waves. The resulting best-fit values for the SED model parameters, and
associated confidence limits, are physically meaningful quantities. The
Iris SED analysis tool allows for robust modeling and fitting of SED
data through association with Sherpa, an extensible, Python-based,
multi-waveband modeling and fitting application for astronomers.

Learn how to fit models to SED data in Iris with custom model
expressions, including preset and/or your own model components; how to
set initial model parameter values and ranges, and choose an appropriate
fit statistic and method; as well as calculate errors on best-fit model
parameters.

**Last Update:** ________ - updated for Iris 3.0. The Fitting Tool has been 
completely redone, encapsulating 

------------------------------------------------------------------------

### <a name="toc"></a>Contents

-   **[Displaying Fitting Options](index.html#open_fit)**
-   **[Defining Model Expressions](index.html#define_model)**
-   **[Setting Model Parameters](index.html#set_pars)**
-   **[Choosing the Fit Statistic and Optimization
    Method](index.html#fit_stats)**
-   **[Defining Fitting Ranges](index.html#fitting-ranges)**
-   **[Fitting and Displaying the Model](index.html#fit)**
-   **[Saving and Restoring the Model](index.html#save)**
-   **[Importing Custom Models](index.html#custom_models)**
    -   [Table Model](index.html#table_model)
    -   [Template Model Library](index.html#template_lib)
    -   [Python User Model](index.html#python_model)
-   **[Integrating Under a Fitted
    Model](index.html#integrate_under_model)**
-   **[History](index.html#history)**

------------------------------------------------------------------------

## <a name="open_fit"></a> Opening the Fitting Tool

After one or more SED data segments and/or photometric points have been
[read into Iris][entry], and [data display preferences
set][plot], the data may be fit with a customized model 
using the **Fitting Tool**. Clicking the Fitting Tool
icon ![Fitting Tool icon][fitting-tool-icon] opens a new 
window in which individual model
components may be combined to define a custom model expression, and where 
initial model parameter values and the
spectral fitting ranges are set. 

Model amplitudes are in units
of photon flux density by default, and model spectral coordinates are in
Angstroms.

[![Iris Screenshot](./imgs/open_fitting_v2_small.jpg)](./imgs/open_fitting_v2.png)

The *Model Components* section of the fitting window lists the
model components used to construct the full model
expression for fitting; these components can then be arbitrarily
combined to form the full model expression, in the *Model Expression*
field. Components are referenced by a model identifier "<tt>m#</tt>", 
where the number increases for each new component added to the Model 
Components list.

|   |
|--:|
|[[Back to top][top]]|

------------------------------------------------------------------------

## <a name="define_model"></a> Defining Model Expressions

Model expressions are defined by combining model components together in the *Model Expression* field at the top of the Fitting Tool frame.

PICTURE HERE

The list of available models is shown on the left-most panel of the Fitting Tool. 
Double-clicking a model will add it to the list of model components. By default, components are linearly combined in the Model Expression field when a model is added.

PICTURE HERE

Iris is distributed with a list of preset optical and X-ray [Sherpa][sherpa] models. A brief description of the model is displayed below the list when the users highlights a model name. More in depth-descriptions of the Sherpa models are discussed in  [Iris Models][models].

There is also the option to choose a custom template,
template library, or Python user model which you may have imported into the
session via the Iris "Custom Models Manager" tool (see "[Importing
Custom Models](#custom_models)" below to learn how to import
custom models into Iris).

![Iris Screenshot](./imgs/preset_modcomps.png)
![Iris Screenshot](./imgs/custom_modcomps.png)

Components may be added or multiplied together arbitrarily, which allows the modeling of emission and/or absorption features as well as the ability to apply a more complex model to the continuum itself. 

For a simple model, such as an expression containing one model component, defining the model is trivial: write the component ID of the model component, e.g., “<tt>m1</tt>”, in the Model Expression field. For a composite model, add, subtract, multiply, and/or divide the model components as needed to model your SED, such as "<tt>m1\*m2 + m3/(4*3.14)</tt>". Note that numbers may be used directly in the model expression as well. 

Consider the example of fitting an absorbed broken power-law model to
an SED of object 3C 273. You would select and add "[atten][atten]" and
"[brokenpowerlaw][brokenpowerlaw]" from the list of preset Iris models, which 
adds both models to the Model Components section of the fitting window.

![Model Components](./imgs/mod_comps.png)

Then, you would define the
model expression as the product of the two components: "<tt>m1\*m2</tt>".

------------------------------------------------------------------------

## <a name="set_pars"></a> Setting Model Parameters

Each component in the Model Components list may be expanded to show each component's model parameters. From here, the user can select the model parameters and set the initial parameter values and ranges by editing the fields shown to the right of the Components list.

![Edit model parameters](./imgs/edit_pars_v2.png)

The parameter <!--units,--> minimum and maximum values <!--, and links to other parameters--> 
may be specified. The "Frozen" checkbox is for specifying whether or not to 
freeze that parameter during the fit; if unchecked, the parameter will be 
allowed to vary. 

*Note: flux and spectral parameter values must be in units of photons/s/cm2/Angstrom and Angstroms, respectively.*

<!--The "Fix all" and "Default Fit" options in the main fitting window may
be used (while the model editor window remains open) to freeze all model
parameters at current values, or thaw all model parameters (even those
initially fixed), respectively.-->

The initial model parameter values are where Sherpa starts the fit in
parameter space; the parameter ranges are the bounds of parameter space.
It is not possible to fit using parameter values outside the specified
parameter ranges.

|   |
|--:|
|[[Back to top][top]]|

------------------------------------------------------------------------

## <a name="fit_stats"></a> Choosing the Fit Statistic and Optimization Method

The next step in the preparation for fitting involves choosing a fit
statistic and optimization method appropriate for your analysis. These methods 
are listed below with brief descriptions. For more detailed descriptions, 
please refer to the [Statistics](/sherpa/statistics/) and 
[Optimization](/sherpa/methods/) pages of the Sherpa website.

![Fitting Tool window](./imgs/fitting.png)

<div style="text-align:center;font-size:1.5em;padding-bottom:10px">Fit Optimization Methods</div>

<table class="item-description table">
<tr>
<th>Optimization Method</th>
<th>Description</th>
</tr>
<tr>
<td>Levenberg-Marquardt</td>
<td>a method to find the best-fit model parameter  values, by finding the local minimum in parameter space; the functions to be minimized are nonlinear least-squares functions, of the model parameters.</td>
</tr>
<tr>
<td>Nelder-Mead</td>
<td>a method to find the best-fit model parameter,values, by finding the local minimum in parameter space; a direct,search method is used to continually move "downhill" in parameter,space, until settling in a local minimum.</td>
</tr>
<tr>
<td>Monte Carlo</td>
<td>a method using the differential evolution,algorithm, to find a global minimum in parameter space; the search,is seeded with randomly selected starting points, and can continue,the search for the true minimum where the other methods could get,stuck in local minima that do not represent the actual best fit.,(Most useful for complex models and fits that could explore,complicated regions of parameter space.)</td>
</tr>
</table>

<!--

| Optimization Method     | Description                                      |

| **Levenberg-Marquardt** | a method to find the best-fit model parameter  values, by finding the local minimum in parameter space; the functions to be minimized are nonlinear least-squares functions, of the model parameters. |
| **Nelder-Mead**         | a method to find the best-fit model parameter,values, by finding the local minimum in parameter space; a direct,search method is used to continually move "downhill" in parameter,space, until settling in a local minimum. |
| **Monte Carlo**         | a method using the differential evolution,algorithm, to find a global minimum in parameter space; the search,is seeded with randomly selected starting points, and can continue,the search for the true minimum where the other methods could get,stuck in local minima that do not represent the actual best fit.,(Most useful for complex models and fits that could explore,complicated regions of parameter space.) |

-->

<div style="text-align:center;font-size:1.5em;padding-bottom:10px">Fit Statistics</div>

<table class="item-description table">
<tr>
<th>Statistic</th>
<th>Description</th>
</tr>
<tr>
<td>Chi2</td>
<td></td>
</tr>
<tr>
<td>Chi2DataVar</td>
<td>Chi-squared statistic with variance computed from the data. If measured errors are provided, the variance is taken from these errors; else, the variance is computed from the y-values of the data points.</td>
</tr>
<tr>
<td>Chi2Gehrels</td>
<td>Chi-squared statistic, where the variance is computed with a function from Gehrels et al. Suitable for low counts data (e.g., X-ray data) to correct for bias in using chi-squared.</td>
</tr>
<tr>
<td>Chi2ModelVariance</td>
<td>Chi-squared statistic, where the variance is computed from the model values instead of data.</td>
</tr>
<tr>
<td>Chi2ConstantVariance</td>
<td>Chi-squared statistic, where the variance is set to be a constant value. That constant is the average of the y-values of the data points.</td>
</tr>
<tr>
<td>Chi2XspecVariance</td>
<td>Chi-squared statistic, where the variance is computed as the X-ray spectral fitting program XSPEC would compute the variance (i.e., where the variance would be less than one, reset it to one). More suitable for low counts data (e.g., X-ray data).</td>
</tr>
<tr>
<td>CStat</td>
<td>A maximum likelihood function similar to Cash, but with a chi-squared-like probability distribution. More suitable for counts data than for fluxes.</td>
</tr>
<tr>
<td>Cash</td>
<td>A maximum likelihood function based on Poisson statistics. More suitable for counts data than for fluxes.</td>
</tr>
<tr>
<td>LeastSquares</td>
<td>Sum of the squares of the differences between, data and model values.</td>
</tr>
</table>

<!--
| Statistic                | Description                                                                                                                                                                                                                                            |

| **Chi2**                 | Chi-squared statistic, where the variance is taken from the errors. If no errors are provided, these data points are excluded from the fit. |
| **Chi2DataVar**          | Similar to **Chi2**. Chi-squared statistic, where the variance is taken from the errors. If no errors are provided, the variance is computed from the y-values of the data points.                                             |
| **Chi2Gehrels**          | Chi-squared statistic, where the variance is computed with a function from [Gehrels et al. (1986)](http://adsabs.harvard.edu/abs/1986ApJ...303..336G). Suitable for low counts data (e.g., X-ray data) to correct for bias in using chi-squared. |
| **Chi2ModelVariance**    | Chi-squared statistic, where the variance is computed from the model values instead of data.                                                                                                                                                           |
| **Chi2ConstantVariance** | Chi-squared statistic, where the variance is set to be a constant value. That constant is the average of the y-values of the data points.                                                                                                              |
| **Chi2XspecVariance**    | Chi-squared statistic, where the variance is computed as the X-ray spectral fitting program XSPEC would compute the variance (i.e., where the variance would be less than one, reset it to one). More suitable for low counts data (e.g., X-ray data). |
| **CStat**                | A maximum likelihood function similar to Cash, but with,a chi-squared-like probability distribution. More suitable for,counts data than for fluxes.                                                                                                    |
| **Cash**                 | A maximum likelihood function based on,Poisson statistics. More suitable for counts data than for fluxes.                                                                                                                                              |
| **LeastSquares**         | Sum of the squares of the differences between, data and model values.                                                                                                                                                                                  |
-->

The default fitting method and statistic are "NelderMead" and
"LeastSquares", respectively, which represent good choices for a robust,
quick, initial fit of a relatively simple model to a data set covering
potentially many orders of magnitude in flux and/or wavelength. The fit
can also be done with a chi-squared statistic or with a maximum likelihood 
statistic useful for data with low number counts. The optimization 
method can be changed to "Levenberg-Marquardt" or "Monte Carlo", but note that switching
the method is less important than switching the statistic, e.g., from
least-squares to chi-squared.

Nelder-Mead is the optimal fitting method to start with because it does
not depend on taking derivatives of the model function. As for the fit
statistic, least-squares is preferred because it does not use measured
errors and thus essentially weights all data points equally (it seeks to
minimize the sum of the squares of the differences between data and
model values, without taking errors into account). Chi-squared fitting,
in contrast, can be decidedly biased towards the data points with the
lowest fluxes and smallest measured error bars. In other words, when there are data
points with measured errors that are orders of magnitude smaller than
the error bars on most of the data points, then these points become the
biggest contributors to the chi-squared value.

In subsequent fits - e.g., after selecting a different data range to
fit, adding in new model components as needed, and so on - the statistic
can be switched to a chi-squared option to use measured errors
(preferably "Chi2" or "Chi2Datavar" for high counts (>5) data points; 
"Chi2Gehrels" or "Chi2XspecVariance" for low counts data). If measured errors 
are provided, the variance is taken directly from the errors provided with the 
data.

**COME BACK HERE!!**

**Note**: When one or multiple SED segments is fit in Iris, any data
points with associated zero-value errors are ignored in the fit. This
design choice is intended as a safeguard against yielding potentially
misleading fit results in the analysis of your SED data. Iris interprets
a *zero-value error* not to mean that the uncertainty on the associated
data value is actually zero, but that *a measure of the uncertainty is
not available for that particular photometric point.*

|   |
|--:|
|[[Back to top][top]]|

------------------------------------------------------------------------

## <a name="fitting-ranges"</a> Defining Fitting Ranges

Before initiating a fit of the defined model to a SED, the
specific subset of the SED data to be included in the fit (if not the
entire SED) may be specified using the "Add Range.." option in the
main fitting window. This opens a *Fitting Ranges* manager window in which a 
user defines the fitting range(s) for the fit.

[![Defining the fitting range](./imgs/define_range_v2_small.jpg)](./imgs/define_range_v2.png)

A fitting range may be defined by two ways: 

- typing the minimum and maximum spectral range values in the *Add Range* box then clicking "Add"
- selecting the "Add from plot" button and setting the min and max spectral ranges by clicking on the plot twice.

Fitting ranges may be removed by highlighting the ranges and clicking "Remove"; all ranges can be removed with the "Clear all" button.

Defining multiple fitting ranges is useful for masking out spectral features 
when fitting the continuum of a spectrum.

|   |
|--:|
|[[Back to top][top]]|

------------------------------------------------------------------------

## <a name="fit"></a> Fitting and Displaying the Model

Having built a model expression and set initial parameter values, chosen
an appropriate fit statistic and optimization method for your analysis,
and defining the range of data to be fit, you are ready to initiate the
fitting process.

Click "Fit" in the Fitting Tool window to start the fit. When the fit
is complete, a red model curve appears overplotted on the SED data in
the Visualizer (Note that the red line may be plotted beyond the specified data 
range to be fit; this extraneous portion of the fitted model may be ignored).

[![SED Viewer with fitted model overplotted](./imgs/model_plot_v2_small.jpg)](./imgs/model_plot_v2.png)

When the fit has finished, the model parameter values will appear
updated in the Model Components fields, and fit statistics
will be displayed in the bottom panel. The fit results include 

- the final fit statistic
- the reduced fit statistic*
- the Q-value (the probability that the fit is consistent with the data)*
- the number of model evaluations done to reach the best fit parameter values
- the number of data points used in the fit
- the degrees of freedom

*The Q-value and reduced statistic are unavailable when fitting with the 
least-squares or Cash, as they cannot be computed for those statistics.

![Statistics](./imgs/fit_saved_v2_small.jpg)
![Fit statistics window](./imgs/fit_stats_leastsq_v2.png)

When fitting with one of the chi-squared statisics, or the
chi-squared-like Cstat statistic, the confidence limits of the fitted model 
parameter values may be calculated. 

Enter the the confidence interval in terms of sigma and click "Compute" to 
calculate the upper and lower confidence limits for the on the best-fit model
parameters. For example, entering "1.6" in the "sigma" field will return the 90%
confidence limits on the model parameter values. The limits are calculated using
the statistic and method chosen for the fit. 

![Confidence limits](./imgs/confidence_chi2.png)

If the statistic is left at the default "leastsq", Iris will issue an
error stating that least-squares cannot be used with the confidence
limit function (this is because the only way calculate to confidence
limits is to know the probability distribution for the fit statistic,
which is known for the chi-squared and chi-squared-lke cstat statistic,
but not least squares).

Also of note is that blank or "NaN" values are returned in the
confidence results when a parameter bound is found to lie outside the
hard limit boundary for a model parameter (which ought not to be changed
by the user, so there is not an option to do so in Iris). This could
result from an issue with the signal-to-noise of the data, the
applicability of the model to the data, systematic errors in the data,
among others things. A parameter hard limit represents either a hard
physical limit (e.g., temperature is not allowed to go below zero), a
mathematical limit (e.g., prevent a number from going to zero or below,
when the log of that number will be taken), or the limit of what a float
or double can hold (the fit should not be driven above or below the
maximum or minimum values a variable can hold).

You can iterate through the fitting process in Iris as many times as
necessary - adding or deleting models from the model expression;
changing parameter values or ranges; including or excluding new points
from the SED - until you find a satisfactory model that best describes
your SED data.

|   |
|--:|
|[[Back to top][top]]|

------------------------------------------------------------------------

## <a name="save"></a> Saving and Restoring Models

Once a spectral model is satisfactorily fitted, the fitted model
parameters can be saved to a local file by making an appropriate selection in 
the File menu of the fitting window.

![Save Model menu](./imgs/fit_write_menu.png)

Selecting *File -&gt; Save Text...* saves the model and fit results to file in 
a human-readable text format. Example output is shown below:

```
$ more 3c273_atten_bpl_active_comps.txt

File: 3C 273

Thu Feb 26 15:46:31 EDT 2015  Iris 2

TARGNAME: 3C 273

Model Expression:
        c1*c2

Fit parameters:
        Final fit statistic:      0.010714114984176791
        Reduced statistic:        nan
        Probability [Q-value]:    nan
        Degrees of freedom:       413.0
        Data points:              419
        Last function evaluation: 394

Component 1:    atten.c1 
       hcol      = 1.0E20     (NaN NaN)                                   
       heiRatio  = 0.04177875 (NaN NaN)                                   
       heiiRatio = 0.74654233 (NaN NaN)                                   

Component 2:    brokenpowerlaw.c2 
   F   refer  = 300000.0                            angstroms             
       ampl   = 0.0062282784 (0.1065081 NaN)                              
       index1 = -0.039390083 (NaN       -4.82435)                         
       index2 = -0.6063001   (2.4033892 NaN)                              
```

Selecting *File -&gt; Save Json...*, instead, saves the model to a file
in Json format that can be read back by the tool in a future data
analysis session.

![Saving a fitted model](./imgs/save_models_cdb.png)

This customized Iris fitting session may be restored by selecting the
*File-&gt;Load Json...* menu option within the Iris fitting window.

![Reloading a saved, fitted model](./imgs/open_models_cdb.png)

Restored models may be evaluated or refit to other SEDs. 

To evaluate a model on an SED (without refitting), open the Fitting Tool, load the Json file into the fitting session, then open the Visualizer and click "Evaluate" (at the bottom of the plot window). This will overplot the model on the data, and recalculate the fit statistics.

|   |
|--:|
|[[Back to top][top]]|

------------------------------------------------------------------------

## <a name="custom_models"></a> Importing Custom Models

As it may be necessary to fit data with a model that does not come
pre-packaged with Iris, the Custom Model Manager interface is available
for configuring and importing your custom table, template, or Python
function user models into the Iris fitting session.

![Custom Model Manager](./imgs/CustomModel.png)

After entering the path to the file containing the custom model
definition, assigning the model component a string ID, and entering the
model parameter information, the custom model component may be
installed. The next time the Fitting Tool is opened, the model can be
selected from the menu of custom model components and added to a model
expression for fitting, under *Add -&gt; Custom Model Components -&gt;
tables -&gt; "your model string ID"*.

The fields of the Custom Model Manager window are described below:

  - **Component ID** - an arbitrary string to identify the custom model for
storage in Iris

  - **"Table" radio button** - identifies the custom model as a table read
from file. The data contained in custom table models must have the same
units that Iris uses internally for modeling and fitting. The x-axis
units must be in Angstroms, and the y-axis units must be in
photons/s/cm^2^/Angstrom.

  - **"Template Library" radio button** - identifies the custom model as a set
of templates read from files. The data contained in custom template
models must have the same units that Iris uses internally for modeling
and fitting. The x-axis units must be in Angstroms, and the y-axis units
must be in photons/s/cm^2^/Angstrom.

  - **"Python Function" radio button** - identifies the custom model as a
function that will be imported from Python

In the text box beneath the radio buttons, type in the full path to the
file containing the custom model, e.g.,
"&lt;your\_path\_to\_file&gt;/mypowlaw.py" for the "Python Function"
option.

  - **Component Parameters -&gt; Function Name** - the name of the Python
function to be added as a user model, used only for the Python Function
option

  - **Component Parameters -&gt; Names** - names of the model parameters,
separated by commas

  - **Component Parameters -&gt; Values** - the initial parameter values
corresponding the parameter names listed above, separated by commas

  - **Component Parameters -&gt; Mins** - the minimum allowed values,
separated by commas.

  - **Component Parameters -&gt; Maxs** - the maximum allowed values,
separated by commas.

  - **Component Parameters -&gt; Fixed** - Boolean values, separated by
commas, indicating whether parameters are fixed at the initial value
during the fit (True = fixed at starting value, False = allowed to vary
during the fit.)

  - **Install Model Component** - install the model as a custom model in Iris.
The next time the Fitting Tool is opened, the model can be selected from
the menu of custom model components, under *Add -&gt; Custom Model
Components -&gt; functions -&gt; "your model component ID"*.

|   |
|--:|
|[[Back to top][top]]|

------------------------------------------------------------------------

### <a name="table_model"></a>  Table Model

Iris supports ASCII-format table model files consisting of two separated
columns of numbers, the X (spectral coordinate) and Y (flux) data
values. When the table model is "calculated" during a fit, it returns
the array of Y values multiplied by a single parameter for the model,
amplitude. The amplitude parameter can be varied during the fit (i.e., a
scale factor applied to the tabular data).

Example entries in the Custom Model Manger window are shown in the image
below for a custom power-law table model.

![Defining a table model](./imgs/define_table.png)
![Adding a table model](./imgs/add_table_small.png)

The example table model file "sed\_temp\_data.dat" - which can be found
in the "examples" directory of your Iris installation - is shown below,
where the X column contains wavelength values in units of Angstroms, and
the Y column is flux density in units of photons/s/cm^2^/Angstrom (the
internal units used for fitting in Iris are always
photons/s/cm^2^Angstrom against Angstroms).

``` {.highlight}
% more <basedir>/miniconda/iris/opt/iris/examples/sed_temp_data.dat

   4.8588736e-06   8.4482890e-03
   1.7739201e-01   4.0325498e-03
   2.0675345e-01   9.2701427e-03
   3.2201128e-01   6.9831383e-03
   3.5436466e-01   9.1989617e-03
   4.1350690e-01   2.8576857e-03
   2.0675345e+00   4.1752139e-03
   2.3793056e+00   6.1398901e-03
   2.4776240e+00   1.1573206e-02
   3.1002327e+00   2.4582868e-03
   6.5314270e+00   3.7663007e-03
   9.2243846e+00   5.8898001e-03
   9.9269040e+00   2.2043961e-03
   1.2388120e+01   1.3400554e-03
   6.1940599e+01   1.1914311e-03
   9.9930833e+02   1.8273482e-02
   1.0302148e+03   3.5890026e-03
        .               .
        .               .
        .               .
```

Clicking "Install Model Component" installs the model as a custom model
in Iris. The next time the Fitting Tool is opened, the model can be
selected from the menu of custom model components, under *Add -&gt;
Custom Model Components -&gt; tables -&gt; my\_sedtab*.

|   |
|--:|
|[[Back to top][top]]|

------------------------------------------------------------------------

### <a name="template_lib"></a>  Template Model Library

Iris also supports template model libraries so that you may compare a
source data spectrum against a set of template models, in order to find
the single template model which best matches the source data. During the
fit, the data are compared to each template, to determine which template
is the closest match to the data. The parameters associated with that
template are returned as the best-fit parameters.

A collection of template models may be read into Iris by entering into
the Custom Model Manager window the name of a single ASCII index file
which lists the file contents of a directory full of template model
files, in addition to the model parameter values associated with each
template file. The various model files should also be in ASCII format,
and contain separated columns of X and Y coordinates, where the X column
lists the wavelength in Angstroms, and the Y column is the flux density
in photons/s/cm^2^/Angstrom.

The Iris Custom Model Manager window would appear as shown below when
loading a template model library, where the template model index
filename is entered into the "Add Custom Model Component" section, and
the template model parameter information is entered into the "Component
Parameters" section. In the "Component Parameters -&gt; Names" field,
the parameter names should match the names listed as parameters in the
template index file.

![Defining a template library](./imgs/define_template.png)
![Adding a template library](./imgs/add_template_small.png)

Clicking "Install Model Component" installs the model as a custom model
in Iris. The next time the Fitting Tool is opened, the model can be
selected from the menu of custom model components, under Add -&gt;
Custom Model Components -&gt; tables -&gt; my\_sedtemp.

Consider the example template model shown below, a representative of a
set of power-law models, where there is a separate model file for each
combination of model parameter values (power-law reference point and
photon index, in this example).

``` {.highlight}
$ ls <basedir>/miniconda/envs/iris/opt/iris/examples/sed_temp_index*.dat

<basedir>/miniconda/envs/iris/opt/iris/examples/sed_temp_index-0.00.dat
<basedir>/miniconda/envs/iris/opt/iris/examples/sed_temp_index-0.10.dat
<basedir>/miniconda/envs/iris/opt/iris/examples/sed_temp_index-0.25.dat
<basedir>/miniconda/envs/iris/opt/iris/examples/sed_temp_index-0.35.dat
<basedir>/miniconda/envs/iris/opt/iris/examples/sed_temp_index-0.50.dat



 
$ ls <basedir>/miniconda/envs/iris/opt/iris/examples/sed_temp_index-0.10.dat

4.8588736000000e-06 1.2188068071007e-03
1.7739201000000e-01 4.2628006741162e-04
2.0675345000000e-01 4.1980069644345e-04
3.2201128000000e-01 4.0160704511216e-04
3.5436466000000e-01 3.9778040979499e-04
4.1350690000000e-01 3.9168789965186e-04
.
.
.

```

Each of the ASCII-format template files listed above contains columns of
wavelength in Angstroms and flux density in photons/s/cm^2^/Angstrom
(the internal units for fitting in Iris are always
photons/s/cm^2^/Angstrom against Angstroms), defining the predicted
power-law spectra emitted by an X-ray source.

The template model index file which is entered into the Custom Model
Manager window should contain a table with one line per template data
file, with three groups of columns in the following order:

-   Model parameter columns (there must be at least two)


-   The MODELFLAG column, which separates the parameter list from the
    filenames/model arrays, marks lines which are to be used or not:
    MODELFLAG = 1 - use the file; MODELFLAG = 0 - do not use the file
    (note that the MODELFLAG column in this file is *not* a
    model parameter)

-   The FILENAME column which points to the data file for that instance,
    including the full directory path to the file.

Iris reads the index file in order to set up the template model with the
parameters specified in the first line, and the arrays from the columns
given by the data files.

An example index file appears below, with model flags (all having value
1) and filenames listed in the two right-most columns, and the power-law
photon index and reference point model parameters listed from the left.
The combination of the two parameter values sets the spectral shape of
the model.

``` {.highlight}
$  more <basedir>/miniconda/envs/iris/opt/iris/examples/sed_templates.dat

# IDX REFER MODELFLAG FILENAME
0.0     5000  1   <basedir>/miniconda/envs/iris/opt/iris/examples/sed_temp_index-0.00.dat
-0.10   5000  1   <basedir>/miniconda/envs/iris/opt/iris/examples/sed_temp_index-0.10.dat
-0.25   5000  1   <basedir>/miniconda/envs/iris/opt/iris/examples/sed_temp_index-0.25.dat
-0.35   5000  1   <basedir>/miniconda/envs/iris/opt/iris/examples/sed_temp_index-0.35.dat
-0.50   5000  1   <basedir>/miniconda/envs/iris/opt/iris/examples/sed_temp_index-0.50.dat
```

Linear interpolation is used by the template model to match the data
grid to the model grid - which must match before the fit statistics can
be calculated for fitting. Instead of a simple grid-search method,
K-nearest neighbor interpolation is used to evaluate the best-fit
parameter values, with k=2 and order=2. The parameter values returned
are a weighted interpolation between two best-fit templates.

|   |
|--:|
|[[Back to top][top]]|

------------------------------------------------------------------------

### <a name="python_model"></a> Python User Model

You also have the option of importing into Iris a custom model function
which you have defined and written in the Python scripting language. The
name of the Python file in which it is saved is entered into the Iris
Custom Model Manager interface with the "Python function" option
selected, as shown below for an example using a power-law function. Note
that the *Component Parameters -&gt; Function Name* field becomes active
when this option is selected.

![Defining a Python model function](./imgs/define_python_function.png)
![Adding a Python model function](./imgs/add_python_function_small.png)

The contents of an example Python user model file is shown below, where
a power-law model function named "mypowlaw" is defined:

``` {.highlight}
$ more powlaw.py

import numpy

def mypowlaw(p, x):
    arg = x / p[0]
    arg = p[1] * numpy.power(arg, p[2])

    return arg
```

The 'p' and 'x' function arguments represent the arrays of parameter
values and x-values, respectively. For this example, the model
parameters entered into the Component Parameters section of the Custom
Model Manager window are the normalization reference point, amplitude,
and photon index of the power-law model. The "Function Name" entered
into this section must match the Python function name in the file,
"mypowlaw".

Clicking "Install Model Component" installs the model as a custom model
in Iris. The next time the Fitting Tool is opened, the model can be
selected from the menu of custom model components, under *Add -&gt;
Custom Model Components -&gt; tables -&gt; my\_py\_powlaw*.

|   |
|--:|
|[[Back to top][top]]|

------------------------------------------------------------------------

## <a name="integrate_under_model"></a> Integrating Under a Fitted Model

After fitting a SED, you can estimate fluxes through user-defined
passbands and photometric filters by integrating under the model
components. This is done from the "Calculate Flux" tab in the Science
tools, which is opened by clicking the ["Shift, Interpolate,
Integrate"][science] icon on the desktop. The user may integrate
under the full model or an arbitrary combination of the model
components. The Fitting Tool must remain open for model integration.

[![\[Calculate Flux
screenshot\]](./imgs/integrate_under_model-default_small.jpg)](./imgs/integrate_under_model-default.png)

After opening the "Calculate Flux" tab, make sure Model Integration is
selected (it should "Integrate Model (YES)"). By default, the full model
will be used to evaluate the fluxes. For our fit of 3c273, the model
expression is `"c1*c2"`. A quick-look view of the model and the
parameter values can be displayed by clicking the "Show Model" button.

[![Calculate Flux
screenshot](./imgs/integrate_under_model-show_model.png)](./imgs/integrate_under_model-show_model.png)

You can change the number of spectral bins used to calculate the
integral by adjusting the value in the "Model evaluation bin \#" box.

By checking-off "Full model," the user can arbitrarily combine the model
components, then integrate the expression in the "Model Expression"
field. This means that users can integrate under *individual model
components*. Multiplication and addition of other model components and
numeric values are acceptable. For example, the expressions
`"c2 * 3.678"`, `"c2 + c1"`, and `"c1 + c2 * 1.2"` are allowed.

Say we want to estimate the total infrared flux and the flux through the
Herschel PACS and SPIRE bands . Going back to the "Calculate Flux" in
the Science tool, we add the Hershcel photometry filters (select
"Photometry Filter" -&gt; "Choose" and search for "Herschel") and add a
user-defined pass band from 0.8 to 1000 microns (8000 - 1E7 Angstroms).
To integrate under the fitted model, we turn "Model Integration" on
(YES), and click "Calculate."

[![Calculate Flux
screenshot](./imgs/integrate_under_model-results_small.jpg)](./imgs/integrate_under_model-results.png)

The results can be exported as a new SED with the "Create SED" button,
or may be saved to a text file with "Save." The text file can be loaded
back into Iris as an ASCII Table.

**NOTE:** If the user exits the main Fitting Tool window, the user will
no longer be able to integrate under the fitted model, as the models
will be lost from closing the fitting session. Iris will ask the user if
they really want to leave the fitting session if they try to close the
Fitting Tool.

|   |
|--:|
|[[Back to top][top]]|

------------------------------------------------------------------------

## <a name="history"></a> History

| Date		   |	Changes				   |
|--------------|---------------------------|
|  09 Aug 2011 |  updated for Beta 2.5 	   |
|  25 Sep 2011 |  updated for Iris 1.0 	   |
|  08 Jun 2012 |  updated for Iris 1.1 	   |
|  02 Jan 2013 |  updated for Iris 1.2 	   |
|  21 Jun 2013 |  updated for Iris 2.0     |
|  05 Aug 2013 |  updated Iris screenshots |
|  02 Dec 2013 |  updated for Iris 2.0.1   |
|  07 May 2015 |  updated for Iris 2.1 beta. Users can now integrate under fitted models. Template library model parameter values are interpolated using k-nearest neighbor with k=2 and order=2. Templates, table models, and functions can all be arbitrarily combined in the Model Expression. |

------------------------------------
 
|   |
|--:|
|[[Back to top][top]]|


<!-- external links -->
[topcat]: http://www.star.bris.ac.uk/~mbt/topcat/#docs "TOPCAT"

<!-- image links -->
[fitting-tool-icon]: ./imgs/fitting-tool-icon-small.png

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
[atten]:			../../references/models.html#atten "atten"
[brokenpowerlaw]:   ../../references/models.html#brokenpowerlaw "brokenpowerlaw"
[powerlaw]:			../../references/models.html#powerlaw "powerlaw"

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