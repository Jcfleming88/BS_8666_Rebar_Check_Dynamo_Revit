# BS-8666-Dynamo-Revit-Check
Check of rebar elements within Revit (using Dynamo) to BS 8666 and with a schedule and visual output

---

![image](https://user-images.githubusercontent.com/64108488/90009319-bc8fcd00-dc95-11ea-9648-39ef1d5f7236.png)

# Description

This set of Dynamo scripts was set up to check the dimensions of rebar modelled within Revit
after it became apparent that Revit itself does not limit the dimensions of rebar to those
set out in BS 8666.

The check pulls dimensions from Revit, checks them against the limits set out in BS 8666 and
then updates custom parameters that the scripts setup. This data is then shown in a schedule
that is setup automatically and highlights any errors in modelling. There is also a simple
colour co-ordinated output produced in the active view. This colour output was used in 3D 
views to help quickly locate bars that were modelled incorrectly.

![image](https://user-images.githubusercontent.com/64108488/90009251-a5e97600-dc95-11ea-8754-6b1f23eaa55f.png)

---

# Requirements

Download the "BIM4Struc" package in Dynamo's package manager before running the scripts. 
The check uses this package to alter how the bars are viewed.

---

# How to Use

1 - Run "Rebar Check Setup.dyn" - This creates custom parameters that will hold data
produced in the check such as the check date, status and error messages.

2 - Run "Rebar Check Schedule.dyn" (optional) - This creates a new schedule that gives a
quick and easy view of any errors in the model.

3 - Go to the view you wish to check the rebar in - I would suggest opening a new 3D view
and setting up the view to show rebar and concrete elements in 60% transparency, hiding all
other elements you don't need to see.

4 - Run "Rebar Check Full.dyn" or "Rebar Check Selected Elements.dyn" - The only difference
in the two scripts is that the "Rebar Check Selected Elements.dyn" requires you to click the
selection node at the start and choose elements that you want to check, the full version
will check all elements. If any rebar elements are grouped then this will stop the script
from running, this is why two scripts were created. This is noted under issues.

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
