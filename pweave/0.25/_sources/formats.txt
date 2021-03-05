
Output Formats
================
.. index:: Output formats

Listing formats
---------------

Pweave supports output in several formats. See the `example gallery <examples/index.html`>__ for examples.

You can list the supported formats using:


.. code-block:: python

    from pweave import PwebFormats
    PwebFormats.listformats()
    

::

    
    Pweave supported output formats:
    
    * html:
       HTML with pygments highlighting
    * leanpub:
       Leanpub markdown
    * markdown:
       Pandoc markdown, same as format pandoc
    * md2html:
       Markdown to HTML using Python-Markdown
    * pandoc:
       Pandoc markdown
    * pandoc2html:
       Markdown to HTML using Pandoc, requires Pandoc in path
    * pandoc2latex:
       Markdown to Latex using Pandoc, requires Pandoc in path
    * rst:
       reStructuredText
    * softcover:
       SoftCover markdown
    * sphinx:
       reStructuredText for Sphinx
    * tex:
       Latex with verbatim for code and results
    * texminted:
       Latex with predefined minted environment for codeblocks
    * texpweave:
       Latex output with user defined formatting using named environments
    (in latex header)
    * texpygments:
       Latex output with pygments highlighted output
    
    More info: http://mpastell.com/pweave/formats.html
    
    
    



Format descriptions
-------------------

.. describe:: rst

  `reStructuredText <http://docutils.sourceforge.net/rst.html>`_ .

.. describe:: tex

  Standard LaTeX. Code, results and terminal blocks are written using
  `verbatim` environment.

.. describe:: texminted

  LaTeX with preset `minted <https://code.google.com/p/minted/>`_ formatting for
  code and results.

.. describe:: texpweave

  LaTeX where code is written using `pweavecode`, results using
  `pweaveout` and terminals using `pweaveterm` environment. The user
  can (and needs to) define the formatting for these environment in
  preamble. This can done e.g. with the `\\newminted` command with `minted
  <https://code.google.com/p/minted/>`_-package.

.. describe:: pandoc

  `Pandoc <http://johnmacfarlane.net/pandoc/>`_ markdown.

.. describe:: sphinx


reStructuredText for `Sphinx <http://sphinx-doc.org/>`_ .

.. describe :: html

  HTML with `pygments <http://pygments.org/>`_ highlighting for
  code. You'll need to add css yourself, here's one option
  `pygments.css <_static/pygments.css>`_ .
