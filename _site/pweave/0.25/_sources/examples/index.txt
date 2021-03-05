
========================
 Pweave example gallery
========================


Basic document: FIR filter design
---------------------------------

This example demonstrates most basic chunk options, output and
capturing figures and it is available in several formats.

.. csv-table:: Example in different formats.
   :header: "Format", "Source", "Pweaved", "HTML", "PDF"
   :widths: 7, 11, 5, 5, 5


   texpygments, :download:`FIR_design_pygments.texw <FIR_design_pygments.texw>` , :download:`open <FIR_design_pygments.tex>` , , :download:`open <FIR_design_pygments.pdf>`
   tex, :download:`FIR_design_verb.texw <FIR_design_verb.texw>`, :download:`open <FIR_design_verb.tex>`, , :download:`open <FIR_design_verb.pdf>`
   texminted, :download:`FIR_design_minted.texw <FIR_design_minted.texw>`, :download:`open <FIR_design_minted.tex>`, ,:download:`open <FIR_design_minted.pdf>`
   rst, :download:`FIR_design.rstw <FIR_design.rstw>`, :download:`open <FIR_design.rst>`, :download:`open <FIR_design_rst.html>`,
   script, :download:`FIR_design.py <FIR_design.py>`, , :download:`open <FIR_design.html>`, :download:`open <FIR_design.pdf>`
   pandoc, :download:`FIR_design.mdw <FIR_design.mdw>`, :download:`open <FIR_design.md>` , :download:`open <FIR_design_pandoc.html>`,





The commands used to process the examples from command line are shown below.

Latex
=====

Pweave has several options for LaTeX output, here is a demonstation of differences:

Latex with pygments syntax highlighting:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:download:`FIR_design_pygments.texw <FIR_design_pygments.texw>`, :download:`FIR_design_pygments.tex <FIR_design_pygments.tex>`, :download:`FIR_design_pygments.pdf <FIR_design_pygments.pdf>`
and with IPython shell :download:`FIR_design_pygments_ipy.pdf <FIR_design_pygments_ipy.pdf>`.


Notice that the first command creates the needed :download:`pygments.sty <pygments.sty>`.
See `pygments docs <http://pygments.org/docs/cmdline/#generating-styles>`__ for more info.


.. code:: shell

    pygmentize -f tex -S default > pygments.sty
    pweave -f texpygments FIR_design_pygments.texw
    pdflatex FIR_design_pygments.tex
    pweave -s ipython -f texpygments FIR_design_pygments.texw
    cp FIR_design_pygments.tex FIR_design_pygments_ipy.tex
    pdflatex FIR_design_pygments_ipy.tex
    



Latex with verbatim output:
~~~~~~~~~~~~~~~~~~~~~~~~~~~

:download:`FIR_design_verb.texw <FIR_design_verb.texw>`, :download:`FIR_design_verb.tex <FIR_design_verb.tex>`, :download:`FIR_design_verb.pdf <FIR_design_verb.pdf>`.


.. code:: shell

    pweave -f tex FIR_design_verb.texw
    pdflatex FIR_design_verb.tex
    



Latex with Minted package for syntax highlighting:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:download:`FIR_design_minted.texw <FIR_design_minted.texw>`, :download:`FIR_design_minted.tex <FIR_design_minted.tex>` , :download:`FIR_design_minted.pdf <FIR_design_minted.pdf>` .


.. code:: shell

    pweave -f texminted FIR_design_minted.texw
    pdflatex -shell-escape FIR_design_minted.tex
    



.. note::

  Using pygments directly from Pweave is much faster than
  using Minted separately.

reStructuredText
================

:download:`FIR_design.rstw <FIR_design.rstw>`, :download:`FIR_design.rst <FIR_design.rst>` , :download:`FIR_design_rst.html <FIR_design_rst.html>`.


.. code:: shell

    pweave FIR_design.rstw
    rst2html.py FIR_design.rst FIR_design_rst.html
    




Published from script
=====================

You can publish documents directly using the `pypublish` command.

Using doxygen mark up:

:download:`FIR_design.py <FIR_design.py>`, :download:`FIR_design.html <FIR_design.html>` , :download:`FIR_design.pdf <FIR_design.pdf>` .

Using cell mark up:

:download:`FIR_design_cells.py <FIR_design.py>`, :download:`FIR_design_cells.html <FIR_design_cells.html>` , :download:`FIR_design_cells.pdf <FIR_design_cells.pdf>` .


.. code:: shell

    pypublish FIR_design.py
    pypublish FIR_design_cells.py
    pypublish -f pdf FIR_design.py
    pypublish -f pdf FIR_design_cells.py
    




Markdown
========

Pandoc
~~~~~~

:download:`FIR_design.mdw <FIR_design.mdw>`, :download:`FIR_design.md <FIR_design.md>` , :download:`FIR_design_pandoc.html <FIR_design_pandoc.html>`


.. code:: shell

    pweave -f pandoc FIR_design.mdw
    pandoc -s --mathjax FIR_design.md -o FIR_design_pandoc.html
    



Python-markdown
~~~~~~~~~~~~~~~

`md2html` and `pandoc2latex` formats produce output that is identical
to pypublish command.

:download:`FIR_design.mdw <FIR_design.mdw>`, :download:`FIR_design.html <FIR_design.html>`


.. code:: shell

    Pweave -f md2html FIR_design_noweb.mdw
    




.. _multi-chunk-example:

Splitting code to multiple chunks
---------------------------------

This example shows how to split code between multiple chunks to write
documentation within a class using `complete` chunk option.

:download:`AR_yw.mdw <AR_yw.mdw>` , :download:`AR_yw.html <AR_yw.html>` , :download:`AR_yw.pdf <AR_yw.pdf>` .


.. code:: shell

    pweave -f md2html AR_yw.mdw
    pweave -f pandoc2latex AR_yw.mdw
    pdflatex AR_yw.tex
    



Octave and Matlab
-----------------

Pweave also supports weaving Octave/Matlab documents similar to Python. The support
is more limited, but it is still useful. See the example below for more info.

:download:`octave_sample.mdw <octave_sample.mdw>` , :download:`octave_sample.md <octave_sample.md>` , :download:`octave_sample.pdf <octave_sample.pdf>` .


.. code:: shell

    pweave -s octave -f pandoc octave_sample.mdw
    pandoc octave_sample.md -o octave_sample.pdf
    



If you have Matlab and "python-matlab-brigde" installed you can use `-s matlab` option.

.. versionadded:: 0.23

Miscellaneous
-------------

Linear regression with Statsmodels: :download:`linear_regression.py <linear_regression.py>`, :download:`linear_regression.html <linear_regression.html>`


.. code:: shell

    pypublish linear_regression.py
    




About the gallery
-----------------

This page is an executable document that be run using Pweave using
IPython shell to run all examples using::

  pweave index.rstw

The latest version of the examples with any required extra files are
available from the `Git <http://github.com/mpastell/pweave-docs/>`__
repository in examples directory.

This gallery was created using:


.. code:: python

    >>> import pweave
    >>> pweave.__version__
    u'0.25'
    >>> import sys
    >>> print(sys.version)
    2.7.11 |Continuum Analytics, Inc.| (default, Dec  6 2015, 18:08:32)
    [GCC 4.4.7 20120313 (Red Hat 4.4.7-1)]
    
    


