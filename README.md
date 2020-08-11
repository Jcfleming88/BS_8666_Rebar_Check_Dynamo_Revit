# BS-8666-Dynamo-Revit-Check
Check of rebar elements within Revit (using Dynamo) to BS 8666 and with a schedule and visual output

---

# Description

This set of Dynamo scripts was set up to check the dimensions of rebar modelled within Revit
after it became apparent that Revit itself does not limit the dimensions of rebar to those
set out in BS 8666.

The check pulls dimensions from Revit, checks them against the limits set out in BS 8666 and
then updates custom parameters that the scripts setup. This data is then shown in a schedule
that is setup automatically and highlights any errors in modelling. There is also a simple
colour co-ordinated output produced in the active view. This colour output was used in 3D 
views to help quickly locate bars that were modelled incorrectly.

---

# How to Use

1 - Run "Rebar Check Setup.dyn" - This creates custom parameters that will hold data
produced in the check such as the check date, status and error messages.

2 - Run "Rebar Check Schedule.dyn" (optional) - This creates a new schedule that give a
quick and easy view of any errors in the model.

3 - Go to the view you wish to check the rebar in - I would suggest opening a new 3D view
and setting up the view to show rebar and concrete elements in 60% transparency, hiding all
other elements you don't need to see.

4 - Run "Rebar Check Full.dyn" or "Rebar Check Selected Elements.dyn" - The only difference
in the two scripts is that the "Rebar Check Selected Elements.dyn" requires you to click the
selection node at the start and choose elements that you want to check, the full version
will check all elements. See the known issues below for why two scripts were written

---

# Known Issues

- Rebar that has been grouped for any reason will prevent the script from running. When
trying to write to the custom parameters, Revit does not allow elements in the group to be
written to. This will stop the script running and abort the whole thing.

>- Fixes
>- Rebar Check Full - Within this script a node has been identified that can be frozen.
Freezing the node will prevent the output data from being written to the bars and prevent
the schedule from updating but will still produce the visual output showing any errors.
>- Rebar Check Selected Elements - This alternative script allows specific bars to be
selected so any grouped elements can be avoided. It also filters out any non rebar
elements so rebar can be selected by simply dragging a box over the elements.

- Certain elements cannot currently be checked. An example of this is when varying length
bars are created. This is because Revit fills the dimension parameters of the bars with
"varying" rather than a length so the dimensions of the bars cannot be pulled.

>- Fixes
>- Currently the only option is to highlight unchecked bars to be checked by hand (they
show as a blue bar in the current setup). It is likely the dimensions are stored in a
different parameter or the rebar elements so it may be possible to find this and update
the script to use this instead, however, some snooping of the parameters would be required
to find this.

---

# Potential Improvements

- The Python block was initially written in a very direct form and can be improved. There
are a number of functions that are repeated. It would be easily possible to check the sizes
of rebar used within the model, calculate the limits and populate a matrix with the limiting
sizes so some functions are only ran once. Although the script runs relatively fast, this
will improve speed for larger models.

- The analysis of the rebar is done largely in a single custom node. It would be possible
to recreate this script in something such as pyRevit by simply copying and pasting the script.
Recreating in pyRevit would allow for a custom toolbar to be created to do the function of
Dynamo, making this a simple button clicking exercise that can be run by people with no
knowledge of Dynamo. The selection of elements, data cleaning, write to parameter and colour
output would need to be recreated in any new script.

- A process can be setup to automatically generate the view for the visual output. This will
prevent any accidental changes to view when running the script (I ran this on rebar drawings
a couple of times and kicked myself every time!)
