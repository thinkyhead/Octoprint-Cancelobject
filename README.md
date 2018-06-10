# OctoPrint-Cancelobject

This plugin allows the user to interactively cancel objects in gcode based on comment tags added by the slicer.
Currently, the only working model is using Simplify3D and including a separate process for each object (or group of
objects) that the user may want to cancel.

![screenshot](./cancelobject.png)
## Setup

Install via the bundled [Plugin Manager](https://github.com/foosel/OctoPrint/wiki/Plugin:-Plugin-Manager)
or manually using this URL:

    https://github.com/paukstelis/OctoPrint-Cancelobject/archive/master.zip

## Configuration
### Settings
* Be default, active object (current object being queued) is displayed in the NavBar.
* Gcode (comma delimited) can be injected before or after the server reaches a cancelled object.
  This may be need for retractions or resetting extrusion distance in some cases.
### Simplify3D
* Create one process for each object or group of models you want to be able to cancel. Assign models to processes.
* Enable 'Allow zeroing of extrusion distance' setting in Gcode Tab.
* It is recommended to add `; process ENDGCODE` at the start of your Ending Script in S3D. Otherwise, if the last object that would be printed has been cancelled this will result in the rest of the ending script being ignored.
### Slic3r (Prusa Edition, 1.40.0-beta) - sequential printing only
* For the start custom GCODE, include at the end: `; process 0`
* For the end custom GCODE, include at the start: `; process ENDGCODE`
* For the between object custom GCODE, include: `; process [current_object_idx]`
* Other changes may also be necessary
