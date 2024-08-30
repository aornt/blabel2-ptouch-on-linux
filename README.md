# blabel2
Brother P-touch labelprinter for Linux

# INTRODUCTION
Blabel2 is build upon the work of Ari from Finland and uses his installation.
The app is only tested with a brother p-touch 2430PC but may work for others.
It is all written in Perl and uses GTK3

Blabel2 is different than the Rademacher version as described bij Henrik Bengtsson because it uses CUPS and PERL.
Maybe the Blabel2 GUI can make use of the Rademacher version as a backend for printing. I did not investigate this.

There are a few bugs in the blabel2 app, but I have no time to investigate. For me all the essentials work.

# INSTALLATION
Connect the brother label-printer with USB

Create a new printer in CUPS with the RAW profile (or ASCII text)

Install the rpm package from blabel

Add the files and directories from blabel2 as described in LOCATION further on in this readme


# LABEL PRINTING WORKFLOW
The app has the mainwindow in which the text and the icons are composed in a labelblok. 

The text can be vertically divided in 1,2,3 or 4 lines with different text.
The each line can independend of the other lines be formatted with a different font, size, underline or strike-true.

The text can be preceeded bij 1 or 2 icons and superseeded bij 1 or 2 icons.
All 4 icons can be different and are selected in the main window.

In the repeat field can a number be given with which to repeat the above labelblok multiple times into a labelblok-set.
Also it is possible to position a divider-icon between the repeated labelbloks.

There is a lost piece of tape (starting spill) at the start of each printed label, this is due how the brother ez-tape hardware system works.
In order to prevent unnecesary printing of these starting spills, it is possible to place the labelbloks and the labelblok-sets in a buffer.
It is done bij the "add buffer" button in the main window and can be done ach often as needed.

If all is ready to print, go click the "buffer preview" button in the main window. This button will be enabled as soon as there is something in the buffer.

In the buffer-preview window it is possible to add a buffer-divider-icon. This will be placed between all buffered labelbloks and labelblok-sets.
This buffer-divider icon can be choosen with the file-choose button in the buffer window.

In the buffer window it is also possible to clear the buffer and to print the buffer.
The buffer is not stored on harddisk and is empty when starting the label app.

There is a limitation on the length the pixelbuffer and therefore the maximum tapelength is about 6100 mm.


# PRESETS
In the mainwindow it is possible to store presets. The items that are stored as preset-item are:
- line 1 to 4
  text
  font
  font-size
  underline
  strike-through
- text-alignment horizontal
- text-alignment vertically
- inverse
- label-icons outer-left, inner-left, inner-right and outer-right
- labelblok-divider
- printer
- tapewidth
- labelblok repeats
- cut off
- buffer divider (*)
- description of the presetconfiguration

(*) saving the buffer divider-icon is only done if one is selected in the buffer window

There are 10 quick-preset buttons, these select fixed filenames with the pattern preset<x>.conf.
The <x> can vary from 0 to 9 according to the label on the buttons
For automatic detection , the preset<x>.conf file has to be located in the directory that is fixed at $HOME/config/blabel/presets
example: $HOME/config/blabel/presets/preset1.conf

The preset can be generated by setting all preset-items to your prefence and typing the file name in the file field, eg. /home/<username>/.config/blabel/presets4/preset1.conf. After clicking the Save-button the preset will be stored at the selected location.

There will be an inventarisation of available preset configurations at start up of the app and only the preset-buttons that have content will be clickable.

The preset1 button is now active and can be used to summon all preset items at once.

After saving (or loading) the first preset it is easy to alter the preset-items that need to be changed, change the presetnumber in the file name (.../preset1.conf > .../preset3.conf) and click the save button. The according presetbutton will then be clickable.

It is also possible to select your own preset configurations on other locations bij selecting them with the preset-filechooser button. These are non-persistent and have to be manually selected each session you want to use them.

In the fixed-width field you can set a fixed length in millimeters. This is the length of a single label. If repeat is used then the total length is the repeat x the fixed length.
The mimimum length is the combined length of the images that are used in the label. If you want to go shorter then you have to change the size of the images.
If the fixed length is not enough to accomodate the text and the images then the text is cut off at the right and the field with the actual length becomes red as a warning.
You can shorten the text or choose a smaller font in order to fit it in the fixed lenght

It is possible to change the standard search location of the map of the preset-configurations and the images in the configuration window. it is just for convenience.

The image files can be anywhere and the complete path is saved in the preset.

Presetconfiguration files can also be anywhere. If you locate them elsewhere it is just more clicking through the directory tree.


# COMMANDLINE
the preset and buffer functionallity is not available on the commandline. 

# LOCATION
- /usr/bin        # The directory with the perlscripts 
  - blabel2         # The new script/app version2 that creates the image
  - blabel2-print   # The updated printing script/app that sends the image to the printer (version 2)
  - blabel          # The original script/app that creates the image (can be erased when you only use version2)
  - blabel-print    # The actual printing script/app that sends the image to the printer (can be erased when you only use version2)
  
- /usr/share/pixmaps/  
  - blabel2.png      # The image in the "about" window
  
- /usr/share/applications/  
  - blabel.desktop  # The desktop icon

- /usr/share/blabel/
  - blabel2.glade   # The app-layout, this is part of the app itself
  
- $HOME/.config/blabel/
  - blabel.json     # The config-file blabel.json preserves the window content on exit of the app. It is not usable as preset file for quick presets or other user presets. It will be overwritten each session.

- $HOME/.config/blabel/presets   # This directory is the location of the presets.
  - XXXXXX.conf # These will be read and written by the app. It is possible to edit them manually.
  - presetX.conf #  The preset files used by the presetbuttons start with a specific file name: preset0.conf upto preset9.conf. These can also be loaded with the "load file" option and then changed onscreen and saved under the same name. They pop-up when the corresponding preset button is pressed.

