visibilityPV
============

Guide
-----

With EDM the `visibilityPV` property is often used to control the whether or
not a widget is visible.
PyDM widgets do not have a specific property for a visibility controlled by a Channel.
Instead, PyDM offers a more powerful capability called ``Rules`` in which one or more
PVs can be used along with an ``expression`` to control certain properties at widgets.

For now, most PyDM widgets allow users to control the following properties via Rules:

    - Enable
    - Visible
    - Opacity
    - Position - X*
    - Position - Y*

.. note::

    Properties marked with * may not be available at all widgets.

Some widgets offer more properties than others due to the significance of the
property to the widget and whether or not it makes sense to allow dynamic modification
of the property via an expression which depends of one or more ``PyDMChannels``.

Example
-------

For this screen, we want to control the visibility of a ``PyDMDrawingCircle``
using a PV ``EDM2PYDM:VIS:CONTROL``) and make the circle widget visible when
the PV value is equal to 1.

.. note::
    This example uses an EPICS database with simulated PVs which can be
    downloaded at the end of this page.

* **Step 1.**

  Let's start by opening Qt Designer and creating a new ``Widget``.

  .. figure:: /_static/how-to/new_widget.gif
     :scale: 100 %
     :align: center

* **Step 2.**

  Now that we have our form, let's go ahead and add the Widgets.

* **Step 2.1**

  The first widget that we will add is the PyDMEnumButton that will control our
  PV.

    #. Drag and drop a ``PyDMEnumButton`` into the form created at **Step 1**.
    #. Set the ``channel`` property to ``ca://EDM2PYDM:VIS:CONTROL``.

* **Step 2.2**

  Let's add the circle drawing widget which will have its visibility controlled
  via the PV.

    #. Drag and drop a ``PyDMDrawingCircle`` next to the ``PyDMEnumButton`` added
       at **Step 2.1**.
    #. Right-click on the circle widget and select ``Edit rules...``.
    #. Click the ``Add Rule`` button.
    #. Set the ``Rule Name`` field to ``Visibility Demo``.
    #. Select ``Visible`` at the property drop down menu.
    #. Click ``Add Channel``.
    #. At the table bellow fill the ``Channel 0`` with: ``ca://EDM2PYDM:VIS:CONTROL``
    #. Leave the ``trigger`` checkbox marked as we want the rule to be calculated
       every time the Channel value changes.
    #. Set the ``expression`` field to: ``ch[0] == 1``.
    #. Click Save.


* **Step 3.**

  Save your file (suggested name as ``visibilityPV.ui``) and test the example above.

  In one terminal run the example EPICS database:

  .. code-block:: bash

     softIoc -d visibilityPV.db

  In another terminal run the example Display:

  .. code-block:: bash

     pydm visibilityPV.ui

  Once you click at the button and switch from Visible to Invisible you will
  notice that the circle disappears.

  .. figure:: /_static/how-to/visibilityPV/visibilityPV.gif
     :scale: 100 %
     :align: center

.. note::
    You can download the UI file using :download:`this link </_static/how-to/visibilityPV/code/visibilityPV.ui>`
    and the EPICS db file using :download:`this other link </_static/how-to/visibilityPV/code/visibilityPV.db>`.
