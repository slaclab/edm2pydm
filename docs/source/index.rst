EDM to PyDM Migration Guide
===========================

`EDM <https://controlssoftware.sns.ornl.gov/edm>`_ (Extensible Display Manager) is used at many EPICS sites to create
reliable, fast displays. It is based on X11/Linux and provides both an editor
for creating pages and a runtime for displaying them.

`PyDM <https://github.com/slaclab/pydm>`_ (Python Display Manager) is a new framework for building control system
graphical user interfaces using Python and Qt.

It provides a system for the drag-and-drop creation of user interfaces using
Qt Designer, and also allows for the creation of displays driven by Python code.

PyDM is intended to span the range from simple displays without any dynamic
behavior to complex high level applications, with the same set of widgets.

Developers can extend the framework with custom widgets for site-specific
tasks, and data plugins for multiple control systems.


.. toctree::
    :maxdepth: 1
    :caption: Introduction

    motivation.rst
    learning.rst

.. toctree::
    :maxdepth: 1
    :caption: How-To

    how-to/colorPV.rst
    how-to/visibilityPV.rst
    
.. toctree::
    :maxdepth: 1
    :caption: Example Run Non-Layout Mode
    
    example-walk-through/start_with_qdesigner.rst
    example-walk-through/convert_existing_edm.rst
    example-walk-through/stylesheets.rst

.. toctree::
   :maxdepth: 1
   :caption: Contributing

   contrib/help.rst
   contrib/requests.rst

.. toctree::
   :maxdepth: 1
   :caption: Links
   :hidden:

   PyDM GitHub <https://github.com/slaclab/pydm>
   SLAC-wide GitHub <https://github.com/slaclab>
   EDM Website <https://controlssoftware.sns.ornl.gov/edm>
