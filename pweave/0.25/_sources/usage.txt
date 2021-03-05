
Pweave Basics
=============

.. index:: source document, output document

Pweave documents
________________

A Pweave input document contains documentation and code separated with special
markup. Pweave supports several input formats for different purposes. All of the
source formats produce identical output for code. You need to tell the input format
to Pweave using `-i` command line option.

Code chunk formats
------------------

noweb
+++++

Noweb syntax for defining code chunks has been adopted from  `Sweave
<http://www.stat.uni-muenchen.de/~leisch/Sweave/>`_.


Code chunk starts with a line marked with ``<<>>=`` or ``<<options>>=`` and end
with line marked with ``@``. The code between the start and end markers
is executed and the output is captured to the output document.

**Example:** A code chunk that saves and displays a 12 cm wide image
and hides the source code:

::

  <<fig = True, width = '12 cm', echo = False>>=
  from pylab import *
  plot(arange(10))
  show()
  @

markdown
++++++++

Pweave can run code from fenced markdown python code blocks. All of the
following are valid ways to define a code chunk:

::

  ```python
  ```{python}
  ```{.python}

..

However options can only be defined in brackets:

::

  ```{python, caption = "Some figure"}


Documentation chunk
-------------------

 The rest of the document is just copied to ouput and can be written with
 several different markup languages. See `formats <formats.html>`_ page for
 a list of supported output formats.

Inline code
-----------

 Pweave supports evaluating inline code in documentation chunks
 using ``<% %>`` (code will be evaluated in place) and ``<%= %>``
 (result of expression will be printed) tags. Inline code will not
 be included in weaved document.

 **Example**: Use inline code to set some matplotlib options.

::

   <%
   import matplotlib
   matplotlib.rcParams.update({'figure.figsize' : (6, 4),
                           'savefig.dpi': 100,
                           'font.size' : 10 })
   %>

.. versionadded:: 0.2

.. index:: options, figures, inline code chunks

Weaving Pweave Documents
________________________

Weaving a Pweave source file produces a document
that contains text and the weaved code together with its
evaluated output.  All of the produced figures are placed in the
'figures/' folder as a default.


**Pweave documents are weaved from the shell with the command:**

.. describe:: Pweave [options] sourcefile

Options:

.. program:: Pweave

.. cmdoption:: --version

   show the version number and exit

.. cmdoption:: -h, --help

   show help message and exit

.. cmdoption:: -f FORMAT, --format FORMAT

   The output format. Available formats: sphinx, pandoc, tex, html,
   rst, texpweave, texminted. See `<http://mpastell.com/pweave/formats.html>`_


.. cmdoption::  -m MPLOTLIB, --matplotlib=MPLOTLIB

   Do you want to use matplotlib (or Sho with Ironpython) true
   (default) or false

.. cmdoption::  -d, --documentation-mode

   Use documentation mode, chunk code and results will be loaded from
   cache and inline code will be hidden

.. cmdoption::  -c, --cache-results

   Cache results to disk for documentation mode

.. cmdoption::  --figure-directory=FIGDIR

   Directory path for matplolib graphics: Default 'figures'

.. cmdoption::  --cache-directory=CACHEDIR

   Directory path for cached results used in documentation mode:
   Default 'cache'

.. cmdoption::  -g FIGFMT, --figure-format=FIGFMT

   Figure format for matplolib graphics: Defaults to 'png' for rst and
   Sphinx html documents and 'pdf' for tex

Weave a document with default options (rst with png figures)

::

  $ pweave ma.Pnw
  Output written to ma.rst


Weave a Latex document with png figures:

::

  $ pweave -f tex -g png source.Pnw

Get options:

::

  $ pweave --help


Tangling Pweave Documents
_________________________

Tangling refers to extracting the source code from Pweave
document. This can be done using Ptangle script::

  $ ptangle file

  $ ptangle ma.pnw
  Tangled code from ma.pnw to ma.py

Caching results
_______________

Pweave has documentation mode (invoked with ``-d``) that caches code
and all results from code chunks so you don't need to rerun the code
when you are only working on documentation. You can cache the results
using the `-c` option, if there are no cached results then
documentation mode will create the cache on first run.  Inline code
chunks will be hidden in documentation mode. Additionally Pweave will
warn you if the code in cached chunks has changed after the last run.


Document types
______________

.. describe:: Source document

   Contains a mixture of documentation and code chunks. Pweave will
   evaluate the code and leave the documentation chunks as they
   are. The documentation chunks can be written either with reST,Latex
   or Pandoc markdown. The source document is processed using
   *Pweave*, which gives us the formatted output document.

.. describe:: Weaved document

   Is produced by Pweave from the source document. Contains the
   documentation, original code, the captured outputof the code and
   optionally captured `matplotlib
   <http://matplotlib.sourceforge.net/>`_ figures.

.. describe:: Source code

   Is produced by Pweave from the source document. Contains the source
   code extracted from the code chunks.

.. index::  syntax, code chunk, documentation chunk
