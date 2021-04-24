Motivation
==========

EDM to PyDM
-----------

Here are some of the major motivation factors into why EDM is being replaced
and why SLAC decided to develop PyDM when other Display Managers exist at the
EPICS community.


- Red Hat Linux to drop support for Motif after 2024 (End of Life and support
  for RHEL7)

- In 2015, `studies were performed <https://confluence.slac.stanford.edu/download/attachments/234162674/EDMReplacementWhitePaper.pdf?version=1&modificationDate=1524846521000&api=v2>`_ to evaluate software to be used as the
  next-generation display manager at SLAC, and `requirements for a new display
  manager <https://confluence.slac.stanford.edu/download/attachments/234162674/Next_Gen_Requirement_Specification.pdf?version=1&modificationDate=1524846518000&api=v2>`_ were compiled from the major users of EDM throughout the lab [2]

- No existing tools met the requirements defined by stakeholders

  - Key Goal: Drag-and-drop creation of displays (EDM style) and the ability to add intelligence (scripting) to displays using the same tool.

- From the `LCLS-II Controls Review Committee <https://slacspace.slac.stanford.edu/sites/reviews/lclsii/controls_apr_2017/Committee%20Documents/CloseoutSlides[2].pptx>`_ (April 2017):

  - “Consider deprecating EDM and Matlab, and use PyDM and Python for all new displays and high level applications.”


Guide
-----

This guide was created with the purpose to bridge the gap for users switching
from EDM to PyDM since some functionality when implemented on PyDM were not
exactly copied from the ones on EDM on purpose to provide better flexibility
and also the usage of more modern techniques.

If you feel like something is missing, an error was found or would like more
details about a certain subject, please feel free to contact the PyDM team at
SLAC and we will do our best to address the issue.
