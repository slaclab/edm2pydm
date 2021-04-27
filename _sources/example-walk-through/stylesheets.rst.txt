	
************************	
Touch Up and Stylesheets
************************
Let's now do some touch up to make it more similar to the EDM screen. One of the ways we already discussed about is the use of an additional stylesheet besides the **default** one we already have with ``PyDM``.

More about Stylesheets
######################
As mentioned priviously, besides changing the stylesheet for individual widgets, we could create a ``.qss`` file with desired stylesheet properties and this can be applied for the entire screen.

There are many examples and a great amount of information online about different styles for different widgets. Whenever you want to change a style of a widget, you can simply search for **QT Stylesheet for ... PushButton** for example and you can copy and paste those styles thay you find online into your own ``.qss`` file. 
There are also free downloadable ``.qss`` files that others have created, with different themes.

In the ``.qss`` file that we previously created, let's add some more styles for the following widgets. Please note that these are very basic styles that try to simulate a bit the EDM style:

* ``PyDMPushButton``::

	QPushButton {
		background-color: rgb(218, 218, 218);
		border: 2px outset rgb(156, 156, 156);
		border-radius: 5px;
	}
	QPushButton:pressed {
		background-color: rgb(199, 199, 199);
		border: 2px inset  rgb(156, 156, 156);
	}
	QPushButton:hover {
		background-color:rgb(240, 240, 240)
	}
	QPushButton:checked{
		background-color: rgb(199, 199, 199);
		border: 2px inset  rgb(156, 156, 156);
	}
	
* ``PyDMLabel``::

	PyDMLabel {
		background-color: rgb(214, 214, 214);
		border-radius: 3px;
	}

* ``PyDMLineEdit``::

	QLineEdit {
		background-color: rgb(204, 204, 204);
		border-color: rgb(156, 156, 156);
		border-style: inset;
		border-width: 2px 1px 1px 2px;
		border-radius: 3px;
	}

	QLineEdit:hover {
		background-color: rgb(186, 186, 186)
	}

* ``QComboBox``::

	QGroupBox {
		border-radius: 5px;
		background-color: rgb(255, 255, 255);
		margin-top: 15px;
	}
	QGroupBox::title {
		background-color: rgb(255, 255, 255);
	}


.. note::
    You can download the ``.qss`` file that we developed in this walk-through from :download:`this link </_static/example-walk-through/my_style.qss>`
    

Now let's try to open our display with this stylesheet again::

	PYDM_STYLESHEET_INCLUDE_DEFAULT=1 pydm -m "DEV=MY:PV:HERE" --stylesheet my_style.qss mgnt_unit2.ui 
	
We should get something like this:

 .. image::  /_static/example-walk-through/pydm/with_stylesheet.PNG
   :scale: 60 %
   :align: center
   
   
Notice how the ``PyDMLabel`` from the top-left corner now has a background color - let's go back and change the color to match the banner color. 

Before we do that, here is a trick we can use to make it easier on us in ``Qt Designer``:

.. note::
	Let's add the information from our `.qss` file, into the main `Form` from our screen - this way we'll have the same styles while working in ``Qt Designer``. By adding them to the ``Form`` they will be applied to all the widgets, as the ``Form`` is the Top Level containing all the widgets:
	
* Right click on the ``Form`` from the right side of the ``Qt Designer`` under the ``Object Inspector`` section above, and select ``Change styleSheet..``:

 .. image::  /_static/example-walk-through/pydm/object_inspector.png
   :scale: 80 %
   :align: center
   
* Copy and paste all the information from our ``my_style.qss`` file in here:

 .. image::  /_static/example-walk-through/pydm/stylesheet_in_designer.PNG
   :scale: 80 %
   :align: center
   
* Click ``Apply``.

.. important::
	Please remove the stylesheet from the `Form` after you are done with ``Qt Designer`` - it is **not** advised to leave it in there if we use a ``.qss`` file as this will take precedence over the ``.qss`` file and could cause style issues later on if we're changing the ``.qss`` file.
	


Now let's go back to our label and fix its background:

* Right click on the label widget and choose ``Change styleSheet`` from ``Qt Designer``, from here let's change the **background-color** and **border-color**:

Use the ``Pick Screen Color`` option and choose the banner color to make it easier:

 .. image::  /_static/example-walk-through/pydm/pick_screen_color.png
   :scale: 80 %
   :align: center


Adjust the size a bit to align with the banner:

 .. image::  /_static/example-walk-through/pydm/label_background.PNG
   :scale: 80 %
   :align: center

One other thing that we could try to simulate is the ``Embedded Display`` widget, adding a background color to it, follow the same steps above for this widget and choose a color for the background:

 .. image::  /_static/example-walk-through/pydm/embeded_stylesheet.PNG
   :scale: 80 %
   :align: center

There are other things you can try to customize here but if you are happy with your screen, let's get rid of the ``Form`` stylesheet from the ``Qt Designer`` as we do not need it anymore:

* Go back to the **Form**'s ``Change styleSheet`` option, select all that is in there and hit ``Delete`` on your keyboard.


Open the screen again, and this is what we should have for now:

 .. image::  /_static/example-walk-through/pydm/finished.PNG
   :scale: 80 %
   :align: center
