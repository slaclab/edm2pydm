Start with Qt Designer
======================

PyDM uses Qt Designer to create the displays.
Open Qt Designer to start working by typing ``designer`` in your bash shell (*assuming you have your environment already setup*)::
	
	designer

This will open a window like this:

.. figure:: /_static/example-walk-through/pydm/qdesigner.png
   :scale: 60 %
   :align: center



Note that by default the ``Widget`` option is selected as highlighted in the picture above, this is what we should start with, just press on the ``create`` button to proceed with creating a new display.



Qt Designer window has 3 main parts:

1. **Left side** – where all the widgets are

   * you can drag and drop these widgets.
2. **Middle area** – the working area

   * contains the window that will eventually become your screen display.
3. **Right side** – properties

   * you can change the properties of the widgets in this area.


Qt Designer comes with default widgets, they do not support PVs!! See some examples of default widgets on the left picture below (your left):

**PyDM** adds widgets that support access to PVs. See some examples of PyDM widgets on the right picture below (your right) – these widgets' names start with ``*PyDM*...``


.. image:: /_static/example-walk-through/pydm/default_widgets_2.PNG
   :width: 49 %
   :scale: 80 %
   :align: left
.. image:: /_static/example-walk-through/pydm/pydm_widgets.PNG
   :width: 49 %
   :scale: 80 %
   :align: right
	

.. important::
	
	When you need to use widgets with PVs, use the PyDM widgets, otherwise, use the Qt Default Widgets.




You can find more information about the Qt Designer `Qt Designer Manual <https://doc.qt.io/qt-5/qtdesigner-manual.html>`_
	
