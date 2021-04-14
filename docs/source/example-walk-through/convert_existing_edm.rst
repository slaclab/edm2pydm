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

	When we open an ``.ui`` file with PyDM we pass in macros using ``-m`` folowed by the macros definition.
	
EDM - toggle title
******************
Change the window title to display the path to the file - **middle click** on the window and select ``Toggle Title``:

.. image::  /_static/example-walk-through/edm/edm_toggle_title.png
   :scale: 100 %
   :align: center

PyDM - toggle title - View File Path
************************************
Change the window title to display the file location – when window is open go to ``View`` -> ``Show File Path`` in **Title Bar**:

.. image::  /_static/example-walk-through/pydm/pydm_view_file_path.png
   :scale: 100 %
   :align: center


Banner
###########################
EDM
****

Most EDM screens will have a banner. Inspect the widget used for this banner by selecting the banner, and left clicking on the it, you will get the properties of a ``Rectangle`` widget:

.. image::  /_static/example-walk-through/edm/banner_rectangle.png
   :scale: 100 %
   :align: center


PyDM - simple banner
********************
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


