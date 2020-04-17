colorPV
=======

Guide
-----

With EDM the `colorPV` property is often used to bring alarm coloring from a different PV.
PyDM widgets do not have a specific property for a coloring/alarm Channel. The pattern to
be used is to add a PyDMFrame widget and add your widget inside of it.

The PyDMFrame has a channel property in which the PV used as `colorPV` at EDM can be
configured. This will make the inner widget be affected by the changes in Alarm associated with
the PyDMFrame.

Example
-------

For this screen, we want add alarm behavior from a PV (``EDM2PYDM:VALUE``) into
a line edit which uses a PV (``EDM2PYDM:NOALARM``) with no alarm information.

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

  The first widget that we will add is the PyDMFrame that will wrap our Line
  Edit later.

    #. Drag and drop a ``PyDMFrame`` into the form created at **Step 1**.
    #. Make it big enough so you can fit the next widget later.
    #. Set the ``alarmSensitiveBorder`` property to ``true/checked``.
    #. Set the ``channel`` property to ``ca://EDM2PYDM:VALUE``.

* **Step 2.2**

  Let's add the Line Edit which will display the other PV value inside of the
  Frame

    #. Drag and drop a ``PyDMLineEdit`` into the ``PyDMFrame`` created at **Step 2.1**.
    #. Set the ``channel`` property to ``ca://EDM2PYDM:NOALARM``.

* **Step 2.3**

  In order to make life easier for the demonstration of this feature, let's add
  a ``PyDMSlider`` so we can control the values of the alarm PV and simulate the
  alarm conditions.

    #. Drag and drop a ``PyDMSlider`` into the form created at **Step 1** below
       the frame (not inside of it).
    #. Set the ``channel`` property to ``ca://EDM2PYDM:VALUE``.


* **Step 3.**

  Save your file (suggested name as ``colorPV.ui``) and test the example above.

  In one terminal run the example EPICS database:

  .. code-block:: bash

     softIoc -d colorPV.db

  In another terminal run the example Display:

  .. code-block:: bash

     pydm colorPV.ui

  Once you move the slider the Frame will now have its border highlighted
  according to the stylesheet defined for alarms.

  .. figure:: /_static/how-to/colorPV/colorPV.gif
     :scale: 100 %
     :align: center


* **Step Bonus**

  You may have noticed that the PyDMFrame only applied the border to itself.
  That is intentionally done to preserve the look and feel of the inner widgets.
  But one can customize how the local PyDMFrame stylesheet property to act upon the
  inner widgets.

  Here is an example in which we set the stylesheet at the ``PyDMFrame`` widget
  to also change the font color of the inner widgets via the ``color`` property
  if the PyDMFrame has the ``alarmSensitiveBorder`` property checked:

  #. Set the ``PyDMFrame`` stylesheet property to the following:

      .. code-block:: css

        /* alarmSeverity
        0 - No Alarm
        1 - Minor Alarm
        2 - Major Alarm
        3 - Invalid Alarm
        4 - Disconnected
        */
        PyDMFrame[alarmSensitiveBorder="true"][alarmSeverity="0"] QWidget {
            color: green;
        }

        PyDMFrame[alarmSensitiveBorder="true"][alarmSeverity="1"] QWidget {
            color: yellow;
        }

        PyDMFrame[alarmSensitiveBorder="true"][alarmSeverity="2"] QWidget {
            color: red;
        }

        PyDMFrame[alarmSensitiveBorder="true"][alarmSeverity="3"] QWidget {
            color: purple;
        }

        PyDMFrame[alarmSensitiveBorder="true"][alarmSeverity="4"] QWidget {
            color: white;
        }

  #. Running the colorPV.ui file with this snippet inside will produce the
     following result:

     .. figure:: /_static/how-to/colorPV/colorPV_bonus.gif
        :scale: 100 %
        :align: center


.. note::
    You can download the UI file using :download:`this link </_static/how-to/colorPV/code/colorPV.ui>`
    and the EPICS db file using :download:`this other link </_static/how-to/colorPV/code/colorPV.db>`.
