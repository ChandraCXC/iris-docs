# Visualizing SED Data in Iris

------------------------------------------------------------------------

## <a name="overview"></a> Overview

#### Synopsis:

The Iris GUI uses the [STILTS][stilts] API for its plotting backend. The tabular and plot displays of SED data are heavily based on [STIL][stil], the library both [TOPCAT][topcat] and STILTS use. This thread presents the various options available for interacting with and customizing the SED data display in the *Iris Visualizer*.

**WARNING** The visualization documentation is currently **OUTDATED**. The text is matches Iris 3.0b2, but the images reflect an older version.

**Last Update:** Jan 03 2017 - Updated text for Iris 3.0.

------------------------------------------------------------------------

### Contents
--------

-   **[Introduction](index.html#intro)**
-   **[Setting Display Preferences](index.html#set_prefs)**
    -   [Adjusting the Coordinates View Port](index.html#wcsviewport)
    -   [Refreshing the Data Plot](index.html#redraw)
    -   [Units](index.html#units)
    -   [Axis Scale](index.html#axis_scale)
    -   [Grid](index.html#grid)
    -   [Plot Legend](index.html#legend)
    -   [Change SED Display Name](index.html#labels)
-   **[Displaying Metadata and Data Values](index.html#metadata)**
    -   [Data tab](index.html#data_metadata)
    -   [Point Metadata tab](index.html#point_metadata)
    -   [Segment Metadata tab](index.html#segment_metadata)
-   **[Selecting and Masking SED Data Points](index.html#mask)**
    -   [Select Points using Metadata Browser](index.html#mask_metadata)
    -   [Select Points from Data Plot](index.html#select_plot)
    -   [Select Points by Boolean operations](index.html#boolean)
-   **[Extracting a Filtered SED](index.html#extract)**
-   **[Co-plotting Separate SEDs](index.html#coplot)**
-   **[Saving Plot Image to File](index.html#save_plot)**
-   **[Iris Interoperability with other Virtual Observatory
    Applications](index.html#broadcast)**
-   **[History](index.html#history)**

------------------------------------------------------------------------

## <a name="intro"></a> Introduction

When SED data is read into Iris, it displays in the Iris Visualizer,
where you can interact with the data plot in various ways. You can open
the Iris Visualizer from the desktop icon "Iris Visualizer." The terms *Iris
Visualizer* and *SED Viewer* are used interchangeably throughout the
documentation. The options available for customizing the data display
are described in this thread.

![Iris screenshot image](./imgs/plot1_3c066a_angs.png)

When multiple segments and/or photometric points have been read into the
Iris session and co-plotted in the main display, it is important to note
that the spectral data are not combined, co-added, or spliced in memory
in any way; the raw data from the multiple input spectrograms/points is
completely preserved in the resulting combination. This means that two
separate SED data segments loaded into Iris for a particular source -
e.g., observed with two different observatories and spanning separate
(or overlapping) spectral ranges - may be offset from one another, as
Iris does not automatically scale, trim, and join the separate segments
to form a seamless SED for the source. This is illustrated in the image
below.

![Iris GUI snapshot](../../imgs/coplot_small.png)


------------------------------------------------------------------------

## <a name="set_prefs"></a>Setting Display Preferences

### <a name="wcsviewport"></a> Adjusting the coordinates view port

The set of widgets in the Visualizer toolbar are available for adjusting the view and orientation of the SED segment(s) within the main display.

#### Zooming in and out

There are a few methods of zooming and out of the view port:

  * ![\[Iris screenshot image\]](./imgs/zoom_buttons.png)  Zoom out/in by 33% from the center of the viewport by clicking the "In" and "Out" buttons at the top of the Visualizer.
  * Zoom in/out from the cursor's position by hovering over the view port scrolling up or down.
  * Hold Shift and click-and-drag the box to zoom into a specific region on the view port.

#### Expanding the view port

  * Expand or contract either the X or Y axis by hovering over the outside of the graph and scrolling up (to expand) or down (to contract). The cursor's position is the reference position for expanding/contracting the axis.
  * Right-click and drag the mouse over the plot to expand/contract the view port along both the X and Y axes.

#### Panning

There are two methods for panning around the view port:

  * Left-click and drag the plot.
  * ![\[Iris screenshot image\]](./imgs/left_right_buttons.png)   Use the four (4) arrow buttons at the top of the plot window to pan the view port up, down, left, and right.

#### Fix the plot coordinates

![Iris screenshot image](./imgs/auto_button.png)

The user may choose to automatically scale the coordinates view port to fully encompass the data each time the plot is refreshed; or, fix the coordinates view port so that all subsequent plot refreshes that result from a data change will take place on a fixed coordinates view port. To choose the behavior, toggle "View --> Fixed" preference.

By default, if any SED changes occur (adding/removing a SED segment, switching SEDs, etc.), the plot ranges will automatically be reset to show every data point in the SED. By fixing the plot, any SED events that happen outside of the Visualizer will not affect the view port plot ranges. The user can still pan, zoom in/out, and reset the plot ranges manually; the plot view will remain unaffected only by SED changes.  

------------------------------------------------------------------------

### <a name="reset"></a> Resetting the Data Plot

![\[Iris screenshot image\]](./imgs/reset_button.png) The "Reset" button is available within the Iris main display for resetting the data plot so that all edges. |


------------------------------------------------------------------------

### <a name="units"></a> Units

![Iris screenshot image](./imgs/set_units_buttons.png) The preferred units for the data display, e.g., "ergs/cm2/s/angstrom" versus "angstrom", may be set using either the "Units" button in the upper-right corner of the main display. This also updates the units shown in the Metadata Browser's "Data" tab.

The "Units" button allows you to choose the spectral and flux/flux density
units to display an SED in. A dialog box populated with all available physical
units will pop up: the left column is for the spectral (X) axis, and the right
column holds the flux/flux density axis. Selecting the desired units and
clicking the "Update" button adjusts the data display to the desired
preference.

![Iris screenshot image](./imgs/set_units.png)

------------------------------------------------------------------------

### <a name="axis_scale"></a> Axis Scale

The X and Y axes can be plotted in linear or logarithmic scales. The user controls the scaling by clicking "View --> Plot Type -->" on the menu bar,  then choosing the scaling.

![Iris screenshot image](./imgs/plot_type_options.png)  

  * Log - plot both X and Y in a logarithmic scale.
  * Linear - plot both X and Y in a linear scale.
  * X Log - plot X in a logarithmic scale, and Y linearly.
  * Y Log - plot Y in a logarithmic scale, and X linearly.

------------------------------------------------------------------------

### <a name="grid"></a>Grid

Selecting the "Grid" option in the main display overlays a coordinate grid onto the main plot.

![Iris screenshot image](./imgs/grid_button.png) [![Iris screenshot image](./imgs/plot2_grid_on_small.png)](./imgs/plot2_grid_on.png)

|   |
|--:|
|[[Back to top][top]]|

------------------------------------------------------------------------

### <a name="legend"></a>Plot legend

Be default, a plot legend is shown in the top-right corner of the plot display. The legend can be hidden/shown by checking the preference "View --> "Show Legend" off and on.

### <a name="labels"></a>Change SED Display Name

By default, the SED Viewer window displays either "Sed" or "Iris
Visualizer" for any file loaded into Iris. This name can be changed in
the SED Builder window. Type the desired name in the bar next to "ID:"
under "Selected SED" then click "Change." From now on, the SED Viewer
window will display the new name on the top bar and on the plot.

  [![Iris screenshot](./imgs/change_sed_name_small.png)](./imgs/change_sed_name.png)   
  [![Iris screenshot](./imgs/change_sed_name2_small.png)](./imgs/change_sed_name2.png)

|   |
|--:|
|[[Back to top][top]]|

------------------------------------------------------------------------

## <a name="metadata"></a> Displaying Metadata and Data Values

Clicking the "Metadata" button in the upper-right corner of the Iris
display opens a window with tabs containing different levels of data and
metadata in the SED.

[![Iris screenshot](./imgs/open_metadata_browser_small.png)](./imgs/open_metadata_browser.png)

The metadata tables may be sorted by clicking the header of the column by
which you would like to sort - once for ascending order, twice for
descending order <!--, and three times to restore the default sorting--> - and
rearranged by clicking and dragging columns left or right. <!--A nested sort
may be achieved by first selecting the column that will set the master
sort, clicking and holding the Control key, and then selecting the
column by which to sort the groups of the master sort.-->

Users can view the metadata of an arbitrary selection of SED Segments from the 
left column. Hold down Shift and click on the Segments you wish to display in 
the Metadata Browser tabs. The rows in the Data and Point Metadata tabs will 
update to the highlighted SED segments.

[![Metadata Browser](./imgs/mb_segment_select_small.png)](./imgs/mb_segment_select.png)

These sections use VOTable [pks1127-14.vot](./pks1127-14.vot) for demonstrating 
the Metadata Browser. Refer to [Loading SED Data into Iris][entry] if you need instructions on 
loading files from disk.

### <a name="data_metadata"></a> Data tab

![Metadata Browser: data tab](./imgs/data_new.png)

The X and Y coordinate values of each SED data point in the Iris display
are contained in the "Spectral Axis" and "Flux Axis" columns of the Data
tab, and reflect the values that are currently plotted in the Iris display;
when the plot units are changed, the Data tab updates accordingly.

|   |
|--:|
|[[Back to top][top]]|

------------------------------------------------------------------------

### <a name="point_metadata"></a> Point Metadata tab

[![Metadata Browser: point metadata tab](./imgs/metadata_new_small.png)](./imgs/metadata_new.png)

When available, the Metadata tab includes many useful pieces of
information about the data points currently displayed. When a SED is
imported from NED, as in the example considered in this thread, the
metadata includes such things as the bibliographic reference code for
each data point, the spectral range covered by instrument used to obtain
data point, data point uncertainty and flux values as they are
published, data point significance values, among other properties. The
full list of metadata information available for each data point will
depend on the specific data sources.

|   |
|--:|
|[[Back to top][top]]|

------------------------------------------------------------------------

### <a name="segment_metadata"></a> Segment Metadata tab

[![Metadata Browser: segment metadata tab](./imgs/mb_segment_metatdata_small.png)](./imgs/mb_segment_metatdata.png)

Metadata that is common to all data points in a SED segment is displayed
under this tab, in a similar table as the one that appears under the
Point Metadata tab.

|   |
|--:|
|[[Back to top][top]]|

------------------------------------------------------------------------

## <a name="mask"></a> Selecting and Masking SED Data Points

Users can filter and mask SED data using various tools in the Metadata Browser. These capabilities can be accessed from the toolbar under "Select --> ", or through the convenience buttons at the bottom of the Browser window. 

![Metadata Browser buttons](./imgs/mb_filter_mask_selection_tools.png)
 
Here is a quick reference list to the Metadata window's filtering tool buttons:

<!--|-|-|
|![Iris screenshot image](./imgs/mb_select_all_button.png) | select all the points in the table|
|![Iris screenshot image](./imgs/mb_invert_selection_button.png) | invert the selection of points|
|![Iris screenshot image](./imgs/mb_clear_selection_button.png) | clear all point selections|
|![Iris screenshot image](./imgs/mb_extract_button.png) | create a new SED out of the selected points|
|![Iris screenshot image](./imgs/mb_mask_button.png) | mask the selected points. These points will be hidden from the plot and will not be included in any fits|
|![Iris screenshot image](./imgs/mb_unmask_button.png) | unmask the selected points.|
|![Iris screenshot image](./imgs/mb_clear_all_button.png) | clear all masks|
|![Iris screenshot image](./imgs/mb_select_points_filter_button.png) | select the rows for which the given [filter expression](#boolean) returns True.| -->

* ![Iris screenshot image](./imgs/mb_select_all_button.png) - select all the points in the table
* ![Iris screenshot image](./imgs/mb_invert_selection_button.png) - invert the selection of points
* ![Iris screenshot image](./imgs/mb_clear_selection_button.png) - clear all point selections
* ![Iris screenshot image](./imgs/mb_extract_button.png) - create a new SED out of the selected points
* ![Iris screenshot image](./imgs/mb_mask_button.png) - mask the selected points. These points will be hidden from the plot and will not be included in any fits
* ![Iris screenshot image](./imgs/mb_unmask_button.png) - unmask the selected points.
* ![Iris screenshot image](./imgs/mb_clear_all_button.png) - clear all masks
* ![Iris screenshot image](./imgs/mb_select_points_filter_button.png) - select the rows for which the given [filter expression](#boolean) returns True.

The subsections below describe in more detail how users may view, filter, and 
extract new datasets from their SEDs.

### <a name="mask_metadata"></a> Selecting Points using Metadata Browser

Data points can be masked from the Iris plot display and fitting sessions
with a number of methods. 

The most basic works by simply selecting the
rows corresponding to these points in any one of the Point Metadata
<!--, Segment Metadata, --> or Data tabs of the Metadata window, and then 
clicking "Mask Points" at the bottom of that window. You can select the
points by clicking the desired rows while pressing the Ctrl/Command key. In 
the display, the selected points will be removed. 

[![Metadata Browser: select points](./imgs/mask_points_random_small.png)](./imgs/mask_points_random.png) [![Metadata Browser: select points](./imgs/mask_points_random2_small.png)](./imgs/mask_points_random2.png)

In the Metadata Browser, masked points are denoted by a checkmark in 
the "Masked" column. The "Masked" column is only present when at least one point 
is masked. Note that this checkbox column is not clickable; to mask/unmask
points, select the rows you wish to edit, then click ![button](./imgs/mb_mask_button.png) or 
![button](./imgs/mb_unmask_button.png).

<!--
The Metadata Browser provides a couple quick selection tools for table rows:
"Select All" selects all the points shown in the current tab. Users can invert 
the selection of points with the "Invert Selection" button. The 
"Clear Selection" button removes the selection state from all rows in the
table, without affecting the plot display. 

To unmask a point, select it in the 
table, then click "Unmask Points" at the bottom of the frame. The "Clear All" 
button removes all selections and masks, restoring the plot and table displays to their original states. 
-->

The Data and Point Metadata tables can be hierarchically sorted by clicking on
specific column headers. Clicking once sorts the rows in ascending order
of that column; the next click sorts it in descending order <!--, and the next
click places the rows back on their original ordering. By holding the
Ctrl key pressed when clicking on a column header, the sorting state of
previously sorted columns is kept unchanged, thus enabling hierarchical
sorting-->. Using that mechanism, rows can be re-ordered together according to
relatively complex selection criteria against column content. This
facilitates the lumping together of the desired rows, that can in turn
be selected and operated upon with the tools described in the preceding
paragraph. 

For example, we can click on the "DataComments" column and easily 
mask data points with values "Recalibrated Data" by holding down the Shift key and clicking the top and bottom of the "Recalibrated Data" block in the table (see figure below).

<!--without uncertainties by holding
down the Shift key and clicking the top and bottom of the "no
uncertainty reported" block in the table (see figure below).-->

[![Iris
screenshot](./imgs/mask_points_column_sort_small.png)](./imgs/mask_points_column_sort.png)

*Note that columns can be re-positioned at will by dragging their headers
horizontally.*

*Also note that string-valued columns are treated in lexical order.
Integer and floating-point-valued columns are treated in numerical
order.*

|   |
|--:|
|[[Back to top][top]]|

------------------------------------------------------------------------

### <a name="select_plot"></a> Select Points from Data Plot

Data point selection can also be performed based on the plot itself,
instead of the table. One way to do that is by clicking on a specific
data point on the display. The corresponding row in both the Point
Metadata and Data tables will be selected. This selection is
non-destructive, meaning that by successively clicking on points on the
display, one can add the rows corresponding to each one, to the set of
selected rows.

<!--Another way is by zooming over the region that contains the points one
wants to select, and then clicking the "Select from plot" button on the
Metadata window. The table rows corresponding to the data points that
show up inside the plot viewport will be added to the selected set of
rows already on the table.-->

[![Iris screenshot](./imgs/select_points_from_plot_click_small.png)](./imgs/select_points_from_plot_click.png)

|   |
|--:|
|[[Back to top][top]]|

------------------------------------------------------------------------

### <a name="boolean"></a> Select Points by Boolean operations

In order to enable even more complex selection criteria though, table
rows can be selected based on the result of an arbitrary Boolean
expression computed on selected column contents. This expression is
entered in the 'Filter Expression' text field, and by hitting
Return, or clicking on the 'Select points' button, the expression is
computed for every row in the table, and the row is selected if the
Boolean result is True. 

<!--**NOT TRUE ANYMORE** Data points selected by the Boolean filter on
one table (metadata or data) are automatically propgated to the other
table.-->

In the expression, columns are referred by their ordering, where the first 
column is 0. Columns are specified by a "`$`" followed by the column number. 
For example, given the table below, one may select the points which have an 
associated uncertainty with

    $4 > 0

then they can mask the points without associated errors by clicking 
"Invert Selection".

[![filter expression selection](./imgs/filter_expression_selection_small.png)](./imgs/filter_expression_selection.png) [![filter expression selection](./imgs/filter_expression_selection_invert_small.png)](./imgs/filter_expression_selection_invert.png)

Columns may be arbitrarily combined in an expression; what is required are 
boolean comparisons with at least one column on the left- or right-hand side. 
Comparisons may be combined with the logical operators `AND`, `OR`, and `NOT`. 
Expressions are evaluated following the basic order of operations. Iris uses 
[javaluator]() under the hood as to evaluate numeric expressions. All 
mathematical operators `(*, /, +, -,^,log(),log10())`  allowed in javaluator 
may be used in the filter expression.

|                 Comparison Operators ||                   Logical Operators |
|-----|-------------------------------:|-----|-------------------------------:|
| ==  |                       equal to | AND |    "and"; intersection of sets |
| !=  |                   not equal to | OR  |            "or"; union of sets |
| >   |                   greater than | NOT | "and not"; subtraction of sets |
| >=  |       greater than or equal to |||
| <   |                      less than |||
| <=  |          less than or equal to |||
[Filter expression field operators]

s

|                    Logical Operators |
|-----|-------------------------------:|
| AND |    "and"; intersection of sets |
| OR  |            "or"; union of sets |
| NOT | "and not"; subtraction of sets |


Here is an example of a more complex filter expression:

    $3 <= $1 * ($2 + 2.0 * $4) AND $4 > 0

This means "select points where the values in column 3 are less than or 
equal to the values of (column 2 plus 2 times column 4), all times column 1. 
Out of these selected points, only pick those whose values in column 4 are 
greater than 0".

[![complex filter expression](./imgs/complex_filter_expression_small.png)](./imgs/complex_filter_expression.png)

**Caveat:** Only numeric columns may be filtered in Iris 3.0. <!--String-valued 
columns will be selectable via Filter Expressions in Iris 3.0.-->

**WARNING:** Currently columns may only be specified by their column order. 
If a user applies a mask to come data points, the new column will push the 
columns over by 1, so that one must add 1 to their column specifiers in the 
filter expression. The same applies for a user re-ordering the columns; if the 

For example, if the column expression is

    $2 > 1.5 * $3
   
and the user moves the third column to the place of the second column, `$2` 
refers to the *current* 2nd column, which was previously column `3`. 

(See more examples of using the Boolean filter in [Co-plotting Separate
SEDs](#coplot))

|   |
|--:|
|[[Back to top][top]]|

------------------------------------------------------------------------

## <a name="extract"></a> Extracting a Filtered SED

The "Extract" function in the Metadata window allows you to go one step
further than simply masking unwanted data points; it allows you to
extract a whole new SED consisting of only the selected data points.

[![Iris screenshot](./imgs/metadata_new_selected_small.png)](./imgs/metadata_new_selected.png)

Making the desired row selections in the Metadata window and then
clicking "Extract" will open a new SED in the SED Builder window named
"FilterSED" - an ID which you can change - which will display in the SED
Viewer.

[![Iris screenshot](./imgs/extracted_sed_new_small.png)](./imgs/extracted_sed_new.png)

|   |
|--:|
|[[Back to top][top]]|

------------------------------------------------------------------------

## <a name="coplot"></a> Co-plotting Separate SEDs

One can simultaneously plot two or more separate SEDs using the Co-plot
function in the SED Viewer. In this example, we will co-plot two out of
the three separate SEDs imported from NED: M82, M87 and NGC7714. Click
the "Display" button on the Viewer toolbar (upper-left corner) and
select "Co-plot." A menu with the list of all SEDs available for
co-plotting will pop up.

  ![Iris screenshot](./imgs/coplot_small_display.png)   
  [![Iris screenshot](./imgs/coplot_menu_sedbuilder_small.png)](./imgs/coplot_menu_sedbuilder.png)

To co-plot, hold-down the Control key (Command key on Mac systems) and
click on the SED names you wish to view, and then click the "Co-plot"
button on the menu (to select all SEDs, click on the first SED,
hold-down the Shift key, click on the last SED, and hit "Co-plot").
Here, we've selected M82 and NGC7714. The Visualizer updates with all
SEDs selected for co-plotting. Each SED is plotted with a different
color, and the color-coding and the names of the SEDs co-plotted are
shown in the legend <!--(which can be deleted with a mouse click)-->(which can 
be hidden by unchecking "View --> Show Legend" in the menu bar). Note that
the axis units may change after co-plotting; use the "Units" button in
the upper-right corner of the SED Viewer if you wish to change the axes
units in co-plot mode.

[![Iris Screenshot](./imgs/coplot3_units_changed_small.png)](./imgs/coplot3_units_changed.png)

In co-plot mode, you can still access the metadata of each photometric
point by clicking on it, and the Metadata Browser (that can be
accessed by clicking on the "Metadata" button in the SED Viewer window)
can be used to explore the distribution of data and metadata for all
photometric points in the plotted SEDs. 

### <a name="coplot-example"></a>Metadata Browser Example with Co-plotted SEDs

In this example, we use the same NED SEDs "M82" and "NGC7714" from above. 

In co-plot mode, the Metadata Browser orders the rows by SED first, then by 
spectral value. This is true for both the Data and Point Metadata tabs. The same
filtering, masking, and selection capabilities are available in co-plot mode.

[![Iris Screenshot](./imgs/coplot4_small.png)](./imgs/coplot4.png)

To restore the original row ordering of the co-plotted table, click on the 
"Index" column in either tab. 

Let's say we're interested in points with
published uncertainties and with flux values larger than 1.0 Jy. We can mask 
out the other points from the plot and the Fitting Tool. 
Click on the "Data" tab and type `$2 > 1.0 AND $4 > 0` into the
Filter Expression field, where `$2` is the Flux\_Value column, in Jy, and `$4` is
Flux\_Error. We then click "Select Points" --> "Invert Selection" --> "Mask Points". 

[![Iris Screenshot](./imgs/coplot5_small.png)](./imgs/coplot5.png)

One can "Extract" the desired points to a new SED. If you masked the points in the example above, you can either 

   * "Clear All" the masked points, type in the filter expression `$2 > 1.0 AND $4 > 0`, click "Select Points", then "Extract"

or 

   * sort the Masked column, click the first unmasked point, hold the Shift key, and select the last unmasked point, then click "Extract."

A new SED, called "FilterSed," is displayed in the
Viewer, and is available for saving, appending and analyzing in the SED
Builder window. The final SED is displayed in the figure below.

[![Iris Screenshot](./imgs/coplot6_small.png)](./imgs/coplot6.png)

|   |
|--:|
|[[Back to top][top]]|

------------------------------------------------------------------------


<!-- 
THIS SECTION CAN GO BACK WHEN THE COLOR-BY-POINTS FUNCTIONALITY IS ADDED.
-->

<!--
## <a name="coloring"></a> Coloring Data Points based on Metadata

The drop selector at the right bottom of the Point Metadata and Data
tabs allows one to pick a specific column and have Iris paint each data
point on the display with a color that linearly maps into the data range
of the chosen column. In the example below, we have selected the
"DataSignificance" column for the NED SED of M82.

[![Iris
Screenshot](./imgs/color_metadata_small.jpg)](./imgs/color_metadata.png)

Floating-point columns are mapped continuously into color space. Integer
and string valued columns are mapped in such a way that the number of
different colors used in the plot is the same as the number of unique
values in the column. String-valued columns are mapped lexically into
color space.

The color space is defined
[here](http://www.cl.cam.ac.uk/teaching/1112/ECAD+Arch/lab2/extensions.html)

-->

## <a name="save_plot"></a> Saving Plot Image to File

The SED data currently displayed in Iris may be printed to a hardcopy
image in either JPG (.jpg), PNG (.png), GIF (.gif) or BITMAP (.bmp)
format, by selecting "File --> Export plot to image file", and making the
desired image format selection. The image will scale to the size and
shape of the plot in the Iris Visualizer.

[![Plotter screenshot](./imgs/export_to_file_small.png)](./imgs/export_to_file.png) 

[![Plotter screenshot](./imgs/export_to_file_types.png)](./imgs/export_to_file_types.png) [![Plotter screenshot](./imgs/m82_fit_mir_template.jpg)](./imgs/m82_fit_mir_template.jpg)

|   |
|--:|
|[[Back to top][top]]|

------------------------------------------------------------------------


<!-- 
THIS SECTION CAN GO BACK WHEN THE APERTURE CORRECTION FUNCTIONALITY IS ADDED.

OR, THIS COULD BE THE SECTION FOR SCALING SEDS / SEGMENTS BY SOME VALUE.
-->

<!--
## <a name="aperture"></a> Simple Aperture Correction

By right-clicking (Ctrl-click on MacOS) on a specific data point on the
Iris display plot, a window containing information for that point is
brought to screen. The window contains tabs that display similar
information as described above for the Point Metadata, Segment Metadata,
and Data tabs for the entire SED, but relative to the selected point
only.

![Iris Screenshot](./imgs/point_metadata.png)

This window has an extra tab named 'Aperture Correction' that enables
one to apply a simple multiplicative flux correction to the data point.

Entering either the desired flux - or the ratio of the desired flux to
the original flux - and clicking the appropriate button will modify the
data point flux. Iris keeps the original flux so successive applications
of this tool will not cause the original flux value to be lost. In that
way, we can always assign a precise meaning to the ratio value.

![Iris Screenshot](./imgs/aperture_correction.png)

The correction can be applied as well to the entire segment to which the
point belongs. Just select the segments ratio button and enter the
desired flux ratio.

One can also apply a flux correction by directly dragging the desired
point on the Iris display plot, holding the Shift key down while
dragging. Note that this feature is always enabled, even when no
Aperture Correction window is on screen.

-->

## <a name="broadcast"></a> Iris Interoperability with other Virtual Observatory Applications

<!-- MAKE SURE THIS FUNCTIONALITY IS ADDED BEFORE 3.0 GOES OUT -->

Iris is able to communicate with other SAMP-enabled applications, such
as Topcat and Aladin. So long as the SAMP status in the lower left-hand
corner of the Iris desktop says "connected", we can transmit tabular
data back-and-forth between Iris and other SAMP-enabled Virtual
Observatory programs.

![Iris screenshot](./imgs/SAMP.png)

Data is transferred between different applications through the
"Broadcast" button. Iris can broadcast data from the SED Builder, which
allows us to send the metadata for SED segments and aggregate SEDs, and
from the Metadata Browser, from which we can select specific data points
to send using the same methods outlined above in this thread (selecting
by column, Boolean filter, selecting from plot, etc.). The button is
located at the top of the SED Builder window, symbolized as a radio
tower, and in the bottom right-hand corner of the Metadata Browser
window.

Say we want to explore the 3C 066A data with published uncertainties in
a program more suitable for tabular data manipulation, for example
Topcat. We first mask data without uncertainties using the Boolean
filter in the Metadata Browser. If Topcat is open (see [TOPCAT
documentation][topcat]), you
should be able to send the table containing all metadata of the selected
subset of points to Topcat by simply clicking on the "Broadcast" button
in the Single Point metadata browser tab (just make sure that Iris is
registered to the SAMP hub by checking whether Iris icon appears in the
lower-right margin of the main Topcat window). At this point, a table of
the metadata of the selected points will appear in the Topcat file list
window, where users will be able to produce scatterplots, histograms,
and harness all of the powerful data manipulation and data discovery
features available in Topcat.

[![Iris
screenshot](./imgs/topcat_example_small.png)](./imgs/topcat_example.png)

|   |
|--:|
|[[Back to top][top]]|

----------------------------------------------------------

## <a name="history"></a> History

| Date		   | Changes						|
|--------------|--------------------------------|
|  08 Aug 2011 |  updated for Iris Beta 2.5		|
|  26 Sep 2011 |  updated for Iris 1.0			|
|  12 Jun 2012 |  updated for Iris 1.1			|
|  27 Nov 2012 |  updated for Iris 1.2			|
|  05 Aug 2013 |  Updated for Iris 2.0. Added co-plot capability, interoperability with SAMP-enabled applications, and saving plot images discussions. Updated screenshots and fixed table of contents. |
|  02 Dec 2013 |  Updated for Iris 2.0.1       |
|  07 May 2015 |  Updated for Iris 2.1 beta.   |
|  Jan 03 2017 |  Updated text for Iris 3.0.   |
|  Feb 03 2017 |  Updated images for Iris 3.0. |

------------------------

|   |
|--:|
|[[Back to top][top]]|

<!-- external links -->
[topcat]: http://www.star.bris.ac.uk/~mbt/topcat/#docs "TOPCAT"
[stils]:  http://www.star.bris.ac.uk/~mbt/stilts/ "STILTS"
[stil]:   http://www.star.bris.ac.uk/~mbt/stil/ "STIL"

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

<!-- Navigation -->
[toc]:				#toc
[top]:      		#top
