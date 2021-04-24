************************************************
Convert an Existing EDM Screen to a PyDM Screen
************************************************

In this section we will go over an existing EDM screen and try to convert it to a PyDM screen.

.. note::

	There are multiple ways one can go about designing a screen in PyDM, therefore in this Walk-through we will merely cover a particular approach but please be aware that there could be other approaches that are better or simply more convenient for you.
	
Let's start with the screen that we want to convert:

.. figure:: /_static/example-walk-through/edm/screen.PNG
   :scale: 100 %
   :align: center
   

The first steps that we want to take when converting an EDM screen, is to go in ``Edit`` mode on the EDM screen and inspect what types of widgets we have so that we know what widgets we should be using in PyDM.

To do this, **middle click** on the EDM screen and select ``Edit`` – see highlighted in blue in the image below:

.. image:: /_static/example-walk-through/edm/edm_edit_mode.png

Now you can inspect individual widgets’ properties by **left clicking** on the widget you want to inspect.


Window Title and Properties
###########################
EDM - Title
***************
Middle click on the background of the window and select Display Properties:

.. image::  /_static/example-walk-through/edm/edm_display_properties.png
   :scale: 100 %
   :align: center

In the Title of the window's properties, you can see that we use a macro ``$(DEV)``, we want to do the same in PyDM.

PyDM - set Title
****************
When selecting the window (in the work area) you will get on the right side of the Qt Designer, the properties of the window. 
Scrolling down in the properties area you will see one called ``windowTitle`` – change the default name (`Form`) to a custom name.

.. image::  /_static/example-walk-through/pydm/pydm_window_properties.png
   :scale: 80 %
   :align: center


.. important::

	In PyDM we define macros with curly brackets instead of parenthesis, e.g.: ``${DEV}``
	
EDM - window dimensions
***********************

.. image::  /_static/example-walk-through/edm/edm_window_dimensions.png
   :scale: 100 %
   :align: center


PyDM - set window dimensions
****************************
From the Properties area, go to the ``Width`` and ``Height`` properties and change them accordingly:

.. image::  /_static/example-walk-through/pydm/pydm_window_dimensions.png
   :scale: 100 %
   :align: center
   
 
Now let’s save the File in PyDM!
Type ``Ctrl+s`` and give the window a proper name, in this case we'll name it the same way as the edm screen:

.. image::  /_static/example-walk-through/pydm/save.png
   :scale: 100 %
   :align: center
   
For a quick check, you can try to open the ``.ui`` file now with ``PyDM``::
	
	pydm -m “DEV=PV:NAME:HERE” mgnt_unit2.ui
	
.. note::

	When we open an ``.ui`` file with PyDM we pass in macros using ``-m`` followed by the macros’ definition.
	
EDM - toggle title
******************
Change the window title to display the path to the file - **middle click** on the window and select ``Toggle Title``:

.. image::  /_static/example-walk-through/edm/edm_toggle_title.png
   :scale: 100 %
   :align: center

PyDM - toggle title - View File Path
************************************
Change the window title to display the file location – when the window is open go to ``View`` -> ``Show File Path`` in **Title Bar**:

.. image::  /_static/example-walk-through/pydm/pydm_view_file_path.png
   :scale: 100 %
   :align: center


Banner
###########################
EDM
****

Most EDM screens will have a banner. Inspect the widget used for this banner by selecting the banner, and left clicking on it, you will get the properties of a ``Rectangle`` widget:

.. image::  /_static/example-walk-through/edm/banner_rectangle.png
   :scale: 100 %
   :align: center


PyDM - banner
**************
There are multiple ways for replicating an EDM banner in PyDM, in this example we will be using a ``QtFrame``. 

Form the left side where the widgets are, drag and drop a ``Frame`` on your window:

.. image::  /_static/example-walk-through/pydm/banner_frame.png
   :scale: 100 %
   :align: center

Change the dimensions to match the EDM banner dimensions and X, Y location from the properties area on the right:

.. image::  /_static/example-walk-through/pydm/pydm_banner_dimensions.png
   :scale: 100 %
   :align: center
   
Let’s add a color: **right click** on the ``QFrame`` Widget, and choose ``Change styleSheet..``:

.. image::  /_static/example-walk-through/pydm/banner_change_stylesheet.png
   :scale: 100 %
   :align: center
   
From the ``Add Color``, choose the down arrow button:

.. image::  /_static/example-walk-through/pydm/banner_color.png
   :scale: 100 %
   :align: center
   
Choose the ``background-color`` and the ``border-color`` one at the time to change the colors, you should see a window that displays the colors after selecting an option:

.. image::  /_static/example-walk-through/pydm/colors.png
   :scale: 100 %
   :align: center
   
Choose a color for each drop-down option you selected, and save it:

.. image::  /_static/example-walk-through/pydm/save_banner_colors.png
   :scale: 100 %
   :align: center
   
   
.. important::

	We will get more into Stylesheets as we go through this walk-through, generally you want to have a ``.qss`` file where you define the stylesheet for all the widgets and point PyDM to that file. For now, please know that the stylesheet changes made in QtDesigner will take precedence over what is defined in the ``.qss`` file.
	
Ideally, besides the default stylesheet that comes with PyDM, we could have a ``.qss`` file per facility, where we can customize the stylesheet to be specific for that facility.
One example of where this comes into play is the ``banner`` widget.

Let's say we want all the banners to have a certain color in one facility. In this case, instead of manually changing the colors for every screen banner from Qt Designer, we could define the banner color in a ``.qss`` file and point PyDM to it:

* First we would have to give a good name to our banner object so we can later access this name when we create the sylesheet, from the properties change the ``objectName`` to something specific:

.. image::  /_static/example-walk-through/pydm/banner_top.PNG
   :scale: 100 %
   :align: center


* Next we want to create a simple ``.qss`` file:


.. image::  /_static/example-walk-through/pydm/my_stylesheet_banner.PNG
   :scale: 100 %
   :align: center
   
.. note::

	Please note in the stylesheet we only change the style for the QFrame which name is ``banner_top``, so this won't apply for any other frames that we have on our screen.

* Now to make sure this works, let's go back to the banner's styleSheet, **right click** on the banner frame and choose ``Change styleSheet...``, then select everything in there and hit ``Delete`` on your keyboard:

.. image::  /_static/example-walk-through/pydm/delete_stylesheet.PNG
   :scale: 100 %
   :align: center

* Save that, and now let's try to open the screen with our ``.qss`` file from your bash shell::

	PYDM_STYLESHEET_INCLUDE_DEFAULT=1 pydm -m "DEV=MY_PV_HERE" --stylesheet my_style.qss mgnt_unit2.ui 

We would get something similar to this:

.. image::  /_static/example-walk-through/pydm/colored_banner.PNG
   :scale: 100 %
   :align: center

.. note::

	We used the ``PYDM_STYLESHEET_INCLUDE_DEFAULT=1`` variable to include both, our customized stylesheet (``my_style.qss``) and the default one that comes with PyDM.



Static Text
###########################
EDM
****
Static Text Example in EDM, looking at the **Magnet Device Display** text:

.. image::  /_static/example-walk-through/edm/edm_magnet_display_text.png
   :scale: 100 %
   :align: center
   
Some of its properties:

.. image::  /_static/example-walk-through/edm/edm_magnet_display_properties.png
   :scale: 100 %
   :align: center

PyDM
*****
For Static Text in PyDM use a ``QLabel``.
Drag and drop a QtLabel:

.. image::  /_static/example-walk-through/pydm/qlabel.png
   :scale: 100 %
   :align: center
   
Double click on the label to edit the text, or change it from the properties on the right:

.. image::  /_static/example-walk-through/pydm/qlabel_text.PNG
   :scale: 100 %
   :align: center

From properties on the left also change the dimensions as well as the position:

.. image::  /_static/example-walk-through/pydm/qlabel_prop.png
   :scale: 100 %
   :align: center
   
   
Scroll down in the properties area and change the ``font`` if you need/want to by clicking on the button next to font as highlighted in blue below. 
	
.. image::  /_static/example-walk-through/pydm/font.png
   :scale: 100 %
   :align: center
   
.. note::
	
	You might not find all the Fonts that we have in EDM, for simplicity, using the default one is best. Be aware that some fonts might be larger or smaller, and some adjustment of widgets' dimensions might be needed because of that.
   
We'll get a window where we can change more font-specific properties:

.. image::  /_static/example-walk-through/pydm/font_prop.png
   :scale: 100 %
   :align: center
   
By default, a ``QLabel`` will not have a background color so in this case we don’t need to worry about setting the background color to match the banner color (not yet at least), but if we need to add a color to the label widget we would follow the same steps as we did for the ``QFrame``:
**Right click** on the label, go to ``Change styleSheet`` and choose a background color for example:

.. image::  /_static/example-walk-through/pydm/qlabel_color.png
   :scale: 100 %
   :align: center
   

EDM - static text with Macro
****************************
Notice the macro in this text: ``$(DEV)``

.. image::  /_static/example-walk-through/edm/edm_text_with_macro.png
   :scale: 100 %
   :align: center


PyDM - text with Macro
**********************
Drag and drop a ``QLabel``, add a macro - ``${DEV}``:

.. image::  /_static/example-walk-through/pydm/pydm_text_with_macro.png
   :scale: 100 %
   :align: center
   
   
Text Control – Non-Editable
############################
EDM
***
Example of Control Text highlighted below in blue:

.. image::  /_static/example-walk-through/edm/edm_control_text_non.png
   :scale: 100 %
   :align: center
   
Some properties:

.. image::  /_static/example-walk-through/edm/edm_control_text_prop.png
   :scale: 70 %
   :align: center
   

PyDM
****
Use a ``PyDMLabel`` for a non-editable **Control Text** in PyDM. Drag and drop a ``PyDMLabel``.
Go through the same process as for a **Static Text** with changing the dimensions, position, and font (if needed).
Expend the font to make it bold from the font down arrow properties:

.. image::  /_static/example-walk-through/pydm/bold_font.png
   :scale: 100 %
   :align: center

Note the extra properties of a ``PyDMLabel`` if you scroll all the way down in the properties area (compared to the ``QLabel``).

Most of the times you will leave default properties for these labels. Note the ``channel`` property – here is where you would insert a PV.

.. image::  /_static/example-walk-through/pydm/pydmlabel_prop.png
   :scale: 100 %
   :align: center
   
Let's add a PV:

.. image::  /_static/example-walk-through/pydm/add_pv.png
   :scale: 100 %
   :align: center


.. important::

	PVs start with ``ca://`` in PyDM.
	
	
.. note::
	
	If we don’t have Qt Designer set to be “Online” we will not see the PVs’ values in QtDesigner. To set the Qt Designer online we need to export this variable to 1:
	
		``export PYDM_DESIGNER_ONLINE=1``


The banner is done, please note that by default every screen in PyDM will come with similar buttons as in EDM, so there are no widgets for these:

.. image::  /_static/example-walk-through/edm/banner_buttons.png
   :scale: 100 %
   :align: center

.. image::  /_static/example-walk-through/pydm/banner_done.PNG
   :scale: 100 %
   :align: center

In PyDM all screens will have this set of menus:

.. image::  /_static/example-walk-through/pydm/menu.png
   :scale: 70 %
   :align: center

Click on ``File`` to get more options and find out more about PyDM:

.. image::  /_static/example-walk-through/pydm/about_pydm.png
   :scale: 100 %
   :align: center
   
Please explore the other menu information and options.


Grouping Things Together
########################
EDM
****
In this example EDM is using a **Rectangle** and a **Static Text** to form an area. 

.. image::  /_static/example-walk-through/edm/edm_group_together.png
   :scale: 80 %
   :align: center

PyDM
*****
In PyDM there are multiple ways to go about grouping things together esthetically.
You could use a ``QLabel`` and a ``Frame`` to imitate what we have in EDM, but for simplicity we'll use a different widget called ``QGroupBox`` – this one already has a text in it and a shaded frame area by default:

.. image::  /_static/example-walk-through/pydm/group_box.png
   :scale: 100 %
   :align: center

Double click on the ``GroupBox`` text to change the text and change the dimensions from the properties on the right.

.. warning::

	Note that when using the ``QGroupBox`` (or a ``Frame``), the X and Y will reset to 0, 0 from the ``QGroupBox``, so you’ll have to account for that when adding widgets in the box, if you don't want to account for that and want to match the X and Y positions as close as possible to EDM's widgets, add the ``GroupBox`` at the end after you are done adding the widgets. 


For example if we wore to skip ahead and add a ``QGroupBox`` at the end, simply drag and drop a ``GroupBox`` on top of what you want to group (this is just an example):
	
	.. image:: /_static/example-walk-through/pydm/group_with_group_box.PNG
	   :scale: 100 %
	   :align: center


	You can also **right click** on it and send it to back so you can access the widgets in it freely:
	
	.. image:: /_static/example-walk-through/pydm/send_to_back.PNG
	   :scale: 100 %
   	   :align: center


   	You can do a similar thing with a ``Frame``, just drag and drop a ``Frame`` and stretch it so it covers the group area:
   	
   	.. image:: /_static/example-walk-through/pydm/group_with_frame.PNG
	   :scale: 100 %
   	   :align: center
   	   

Meter Widget
########################
EDM
****
.. image::  /_static/example-walk-through/edm/meter_widget.png
   :scale: 80 %
   :align: center
   
PyDM:
*****
In PyDM we do not have a ``Meter`` Widget - we have a similar widget we can use, but the design is a bit different, in the sense that it is not circular, here we can use a ``PyDMScaleIndicator`` widget:

.. image::  /_static/example-walk-through/pydm/scale_indicator.png
   :scale: 80 %
   :align: center
   
Change the dimensions and properties as we previously did with other widgets, add PV:

.. image::  /_static/example-walk-through/pydm/scale_indicator_pv.png
   :scale: 100 %
   :align: center
   
Take off the ``precisionFromPV`` option and add a precision value of 2:

.. image::  /_static/example-walk-through/pydm/scale_indicator_precision.png
   :scale: 100 %
   :align: center
   
Change the color of the indicator if desired:

.. image::  /_static/example-walk-through/pydm/scale_indicator_color.png
   :scale: 100 %
   :align: center
   
You can also get a feel of how it would look in ``Preview Mode``, go to ``Form`` and select ``Preview``:

.. image::  /_static/example-walk-through/pydm/preview_mode.png
   :scale: 100 %
   :align: center

Now if you like how it looks, you can copy and paste it to get the second one.
Select the widget, ``Ctrl+c`` to copy it, and ``Ctrl+v`` to paste it. You will have to adjust the position for the second one and change the PV.

Note that this widget does not have a label, so let’s add a simple ``QLabel``. Place a label right below the widget and make sure it has the same width, as well as it starts at the same X as the scale widget, and at Y + height of scaleIndicator for Y position:

.. image::  /_static/example-walk-through/pydm/scale_indicator_label.png
   :scale: 100 %
   :align: center

Additionally, you can give both these widgets a background color if wanted - to look like they are part of one widget (simulating EDM), just right click on the widget and select ``Change stylesheet`` to add a ``background-color`` and a ``border-color`` for both. Here is how they would approximately look:

.. image::  /_static/example-walk-through/pydm/scale_indicator_grey.png
   :scale: 100 %
   :align: center
   
.. note::

	You can choose a color by picking directly one around your work area by selecting the ``Pick Screen Color``. This is useful when you don’t remember what color you used previously but want them to match with a color you already chose previously - see below:
   
.. image::  /_static/example-walk-through/pydm/pick_screen_color.png
   :scale: 100 %
   :align: center
 
 
Text Control – Editable- Motif Widget 
#####################################
EDM
***
Proceeding with the next section on our screen, we have a widget ``Text Control`` that is in ``Editable`` mode highlighted in blue below:

.. image::  /_static/example-walk-through/edm/control_text_editable.png
   :scale: 100 %
   :align: center
   
PyDM
****
In PyDM, we use a ``PyDMLineEdit`` for a **Text Control** that is **Editable** (you can write in it):


 .. image::  /_static/example-walk-through/pydm/edit_line.png
   :scale: 80 %
   :align: center

It will have similar and additional properties as a ``PyDMLabel``.

* Note how I added the the other labels, we already covered those labels in this walk-through above. If you need to change one thing for multiple widgets of the same type, you can select all of them (mouse drag or Ctrl+left click) and change it for all at once, for example I took out the ``alarmSensitiveBorder`` property Off from the EGU labels:

Select all those labels (``Ctrl+right click`` on the widget):

 .. image::  /_static/example-walk-through/pydm/egu_labels.png
   :scale: 100 %
   :align: center
   
Uncheck the ``alarmSensitiveBorder`` box, unchecking only once will uncheck for all those selected widgets:

 .. image::  /_static/example-walk-through/pydm/uncheck.png
   :scale: 100 %
   :align: center


One thing that I also had to go back and do was to change the **Display Format** for some label widgets, you can do it by selecting multiple widgets again and change the property of the ``dispalyFormat`` to what the EDMs are - in this case I changed them from *Default* to *String*:


 .. image::  /_static/example-walk-through/pydm/display_format.png
   :scale: 100 %
   :align: center


Related Display
###############
EDM
***
Continuing with the next section in the screen we have a new widget that we have not covered here yet - the **Related Display**.

 .. image::  /_static/example-walk-through/edm/edm_related_display.png
   :scale: 80 %
   :align: center



PyDM
****
In PyDM we have a **Related Display** widget called ``PyDMRelatedDisplayButoon`` – this is a button to open another **PyDM** Display.

In addition to this we also have the ``PyDMEDMDisplayButton`` – this is a button to open an **EDM** screen.

In this case, we want to open existing ``.edl`` screens so we will choose the second option:


 .. image::  /_static/example-walk-through/pydm/pydm_related_display.png
   :scale: 80 %
   :align: center
   
From the related button properties, we can add the name to be displayed on the button under the text area:

 .. image::  /_static/example-walk-through/pydm/related_name.png
   :scale: 100 %
   :align: center
   
We can add the filename we want to open, under the ``filenames`` click on ``Change String List``:
   
 .. image::  /_static/example-walk-through/pydm/related_filename.png
   :scale: 100 %
   :align: center
   
Click on ``New`` to add a file and type the file name in the ``Value`` section:

 .. image::  /_static/example-walk-through/pydm/related_dialog.png
   :scale: 100 %
   :align: center
   
.. important::

	Note you have to write the path to this file relative to your current screen.
	
We can also define the related display file’s macros:

 .. image::  /_static/example-walk-through/pydm/related_macros.png
   :scale: 80 %
   :align: center

Check the ``openInNewWindow`` option to open the file in a new window:

 .. image::  /_static/example-walk-through/pydm/related_new_window.png
   :scale: 80 %
   :align: center

Again, as previously mentioned, when we have multiple widgets of the same type and you want to check a box or write the same macros for example, just select all of them and do it all at the same time by writing it only in one spot.


Slider
######
EDM
***
In the next section we meet a new widget that we have not discussed previously, the ``Motif Slider``:

 .. image::  /_static/example-walk-through/edm/motif_slider.png
   :scale: 80 %
   :align: center


PyDM
****
In PyDM we have a similar widget called ``PyDMSlider`` – drag and drop one in the new ``QControlBox`` (note we created a new QControlBox rather than doing that at the end as explained previously):

 .. image::  /_static/example-walk-through/pydm/slider.png
   :scale: 100 %
   :align: center
   
Let's adjust some properties, let's change precision to 4 and take out the ``precisionFromPV``, aslo let's add a ``channel`` PV:

 .. image::  /_static/example-walk-through/pydm/slider_prop.png
   :scale: 100 %
   :align: center
   
Let's also add a label on top of this widget to imitate what we have in EDM:

 .. image::  /_static/example-walk-through/pydm/slider_label.png
   :scale: 100 %
   :align: center


Message Button - Push Button
############################
EDM
***
The Message Button in EDM:

 .. image::  /_static/example-walk-through/edm/edm_push_button.png
   :scale: 100 %
   :align: center
  
Properties.

Notice here the Visibility PV:


 .. image::  /_static/example-walk-through/edm/edm_push_button_prop.png
   :scale: 80 %
   :align: center

   
PyDM
****
In PyDM we would use a ``PyDMPushButton`` for this type of widget:


 .. image::  /_static/example-walk-through/pydm/pydm_push_button.PNG
   :scale: 90 %
   :align: center
   
In our case we might want to change a few main properties like: **text**, **channel**, **pressValue**, **releaseValue**, and maybe others.

 .. image::  /_static/example-walk-through/pydm/push_button_prop.png
   :scale: 90 %
   :align: center


For the **Visibility PV** we would handle it this way in PyDM - **Right click** on the widget and select ``Edit Rule``:

 .. image::  /_static/example-walk-through/pydm/edit_rules.png
   :scale: 100 %
   :align: center
   
   
You will get a new little window where you will need to:

* click on Add Rule
* give it a Rule name 
* add the channel PV 
* define the condition

If you look at the EDM condition, it says **Not Visible** if the PV `value >= 1 and < 2`. 
We will have to modify the condition to be ``true`` for **Visible if** instead:

 .. image::  /_static/example-walk-through/pydm/rule.png
   :scale: 100 %
   :align: center
   
Save it when you are ready. 

.. note::

	For the 3 buttons I applied the same rule, so I was able to select all three buttons and just type the rule ones – this was applied for all 3.
	
	
Menu Button
###########
EDM
***
The next widget we’re going to look at is a **Menu Button**:

 .. image::  /_static/example-walk-through/edm/menu_button.png
   :scale: 80 %
   :align: center

PyDM
****
In PyDM we handle this with the ``PyDMEnumComboBox`` widget:

 .. image::  /_static/example-walk-through/pydm/enum_combo_box.PNG
   :scale: 100 %
   :align: center
   
   
Let's inspect the properties on the right:

 .. image::  /_static/example-walk-through/pydm/enum_combo_box_prop.png
   :scale: 100 %
   :align: center

Take the ``alarmSensitiveBorder`` off here, and add a ``channel`` PV:

 .. image::  /_static/example-walk-through/pydm/enum_button_channel.png
   :scale: 100 %
   :align: center
   
   
Horizontal Bar
##############
EDM
***
**Horizontal Bar** in EDM and its properties:

 .. image::  /_static/example-walk-through/edm/horizontal_bar.png
   :scale: 100 %
   :align: center


PyDM
****
In PyDM we can use the ``PyDMScaleIndicator`` for this type of widget:

 .. image::  /_static/example-walk-through/pydm/scale_indicator.png
   :scale: 80 %
   :align: center


Note, we should check the ``barIndicator`` for it to look like a progress bar, Also, we can change the ``indicatorColor`` to be green, and take the ``showTicks`` off:

 .. image::  /_static/example-walk-through/pydm/bar_indicator.png
   :scale: 100 %
   :align: center

By default this scale indicator will be horizontal, but we can change the ``orientation`` to **Vertical** if we need to.


We can also take the ``showLimits`` off to be more consistent with the EDM widget, as well as ``showValue`` off, and let's also check the ``originAtZero`` box:

 .. image::  /_static/example-walk-through/pydm/bar_prop.png
   :scale: 100 %
   :align: center
   
.. note::

	In Qt Designer it will not show the green progress indicator unless we are reading that PV and it has a value in it.
	
Let’s also add a label:

 .. image::  /_static/example-walk-through/pydm/bar_label.png
   :scale: 100 %
   :align: center
   
  
Choice Button
#############
EMD
***
**Choice button** in EDM in Edit mode:

 .. image::  /_static/example-walk-through/edm/edm_choice_edit.png
   :scale: 100 %
   :align: center
   
**Choice button** in EDM in Exec mode:

 .. image::  /_static/example-walk-through/edm/edm_choice_exec.png
   :scale: 100 %
   :align: center

Properties:

 .. image::  /_static/example-walk-through/edm/choice_prop.png
   :scale: 100 %
   :align: center
   
PyDM
****
In PyDM we would use a ``PyDMEnumButton`` for this widget:

 .. image::  /_static/example-walk-through/pydm/enum_button.PNG
   :scale: 100 %
   :align: center


Properties - please note that besides changing the width and height, we should take off the ``alarmSensitiveBorder``, insert the channel, change the ``orientation`` to **Horizontal**, and set the **margins** settings all to 2 so there is little space between the buttons – imitating the EDM widget:

 .. image::  /_static/example-walk-through/pydm/enum_prop.png
   :scale: 100 %
   :align: center
   
   
Rectangles - Frames
###################
EDM
***
In EDM we have rectangles that let us visually separate sections:

 .. image::  /_static/example-walk-through/edm/edm_rectangle.png
   :scale: 100 %
   :align: center
   
   
PyDM
****
In PyDM we can accomplish the same thing with a ``QFrame``:

 .. image::  /_static/example-walk-through/pydm/frame.png
   :scale: 100 %
   :align: center
   
Adjust the width and height and copy and paste the frame to reuse it. 
You can also change the style of these frames by choosing a different ``frameShape``:

  
 .. image::  /_static/example-walk-through/pydm/frame_shape.png
   :scale: 100 %
   :align: center

Here we chose a ``Box`` and also set the ``frameShodow`` to **Plain** and ``lineWidgth`` to 2:

 .. image::  /_static/example-walk-through/pydm/frame_prop.png
   :scale: 100 %
   :align: center
   
   
This is approximately how it will look:

 .. image::  /_static/example-walk-through/pydm/frames.png
   :scale: 100 %
   :align: center
   
We can also take a different approach here, and instead of creating three boxes, we could create one and add some horizontal lines, and from the properties give them different thickness to be more pronounced if needed.

 .. image::  /_static/example-walk-through/pydm/horizontal_line.PNG
   :scale: 100 %
   :align: center


Radio Button 
############
EDM
***
**Radio Button** in EDM:

 .. image::  /_static/example-walk-through/edm/edm_radio_button.png
   :scale: 100 %
   :align: center


Note if more widgets are in a **Group Box**, you’ll have to middle click and select ``Ungroup`` for all the groups until you get to the ``Radio Box``:


 .. image::  /_static/example-walk-through/edm/edm_group_box.png
   :scale: 100 %
   :align: center
   
Properties of the ``Radio Box``:

 .. image::  /_static/example-walk-through/edm/radio_box_prop.png
   :scale: 100 %
   :align: center

PyDM
****
In PyDM we will use a ``PyDMEnumButton`` for this widget as well:

 .. image::  /_static/example-walk-through/pydm/enum_button.PNG
   :scale: 100 %
   :align: center
   
Set the `widgetType` to ``RadioButton``:

 .. image::  /_static/example-walk-through/pydm/radio_button.png
   :scale: 100 %
   :align: center


Also change the margins from 9 to probably a smaller value, except you want to have some distance vertically between them, so leave the ``verticalSpacing`` to 9.

 .. image::  /_static/example-walk-through/pydm/vertical_space.png
   :scale: 100 %
   :align: center

Besides inserting the channels, some of these radio buttons have a rule - to be invisible when a condition is met, so let’s select all the widgets that will have this rule (the rule is the same for all in this case) and add it in:
Select all radio button widgets that will have the rule. You can select them with holding down ``Ctrl`` and clicking on the widget with the mouse:


 .. image::  /_static/example-walk-through/pydm/radio_button_rule.png
   :scale: 100 %
   :align: center
   
Add the rule by right clicking and choosing Edit Rule:

 .. image::  /_static/example-walk-through/pydm/radio_button_add_rule.png
   :scale: 100 %
   :align: center


Embeded Display
###############
EDM
***
The last portion on this screen that we have not covered yet is the ``Embedded Display``, looking at the properties, we see that this embedded display is opening a file highlighted below:

 .. image::  /_static/example-walk-through/edm/embeded_widndow.PNG
   :scale: 100 %
   :align: center


Notice that we're using a macro here ``$(DISP)`` - if you are unsure of what this macro represents and you have to specify that in a ``PyDM`` embedded display, you can see the macros by right-clicking on the widget, and choose ``Show Macros``

Also, if we need to investigate the ``Related Display Buttons`` a little further, we could open the actual edm screen from the terminal and look at the properties of those buttons::

	edm mgnt_unit_epcs.edl           

This will open the following window in ``Edit`` mode, so we can click on each widget to see their properties:

 .. image::  /_static/example-walk-through/edm/open_edl_screen.PNG
   :scale: 70 %
   :align: center
   


PyDM
****
In ``PyDM`` we'll have to create that file first. Go to ``File`` -> ``New`` and create a new ``Widget``, set the width and height to correspond to the ones seen in the EDM Embedded Display properties.

 .. image::  /_static/example-walk-through/pydm/new_file.PNG
   :scale: 70 %
   :align: center
   
Notice that in the EDM Embedded Display we have 4 **Related Display Buttons**, let's recreate them in ``PyDM``. We'll be using a widget we already covered previously - the ``PyDMEDMDisplayButton`` to open existing edm displays, thus we will not go into too many details here.
Open the displays by clicking on the EDM buttons (from the EDM screen) to see what files we need to open with the Related Display widgets by looking at the ``Toggle Path`` option as previously explained, so we can add those file names and their paths to our ``PyDMEDMDisplayButton`` widgets.

Add their file names:

 .. image::  /_static/example-walk-through/pydm/edm_display_buttons.PNG
   :scale: 60 %
   :align: center

Preview:

 .. image::  /_static/example-walk-through/pydm/epsc_file.PNG
   :scale: 60 %
   :align: center

.. note::
	Make sure you check the ``openInNewWindow`` option for each button!
	
	
Now that we have this file created, let's go back to our main screen and add a ``PyDmEmbeddedDisplay`` widget:

 .. image::  /_static/example-walk-through/pydm/pydm_embeded_display.PNG
   :scale: 60 %
   :align: center
   
Let's add the file name that we just created, and because they are in the same folder, no additional paths need to be included in the ``filename`` properties, only the file name itself.

You'll notice that as soon as you add the filename the display we created previously will appear  on the main screen:

 .. image::  /_static/example-walk-through/pydm/embeded_display.PNG
   :scale: 60 %
   :align: center

.. note::
	If the display is not showing up, make sure the path of the file relative to the current screen is correct!
	

This concludes all the widgets on this screen - go to the next section for some touch up and stylesheets!! And this is approximately  how it looks now:

 .. image::  /_static/example-walk-through/pydm/approximate.PNG
   :scale: 60 %
   :align: center
   
.. note::
	Some of the widgets are disabled because we only have Write-Only access.
	

