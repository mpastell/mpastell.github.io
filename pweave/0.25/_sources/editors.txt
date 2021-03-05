
Editor support
==============

Atom
----

I have made a package for Atom that does syntax highlighting for Pweave documents
it is called `language-weave <https://atom.io/packages/language-weave>`_ and you can
install it from Atom or using apm:


::
      
      apm install language-weave



I use `Markdown Preview Plus <https://atom.io/packages/markdown-preview-plus>`_
without pandoc allows preview of the source document (without syntax highlighting).


Emacs
-----

A good option editing Pweave files with noweb syntax is Emacs using the noweb-mode.
I use .rstw for Pweave documents written with reST markup and .texw for LaTeX markup.
Here is what I have in my ~/.emacs.d/init.el to make Emacs recognize my Pweave documents correctly.

::

   ;Pnw-mode for Pweave reST documents
   (defun Pnw-mode ()
     	  (require 'noweb-font-lock-mode)
          (noweb-mode)
	  (setq noweb-default-code-mode 'python-mode)
          (setq noweb-doc-mode 'rst-mode))

   (setq auto-mode-alist (append (list (cons "\\.rstw$" 'rstw-mode))
		      auto-mode-alist))

   ;Plw-mode for Pweave Latex documents
   (defun Plw-mode ()
   	  (require 'noweb-font-lock-mode)
  	  (noweb-mode)
   	  (setq noweb-default-code-mode 'python-mode)
  	  (setq noweb-doc-mode 'latex-mode))

   (setq auto-mode-alist (append (list (cons "\\.texw$" 'texw-mode))
		      auto-mode-alist))



The code simply sets the documentation mode (*noweb-doc-mode as rst-mode*) as reStructuredText or LaTeX depending on the extension and the code mode as Python, so that the code chunks will be correctly formatted.

VIM
---

Pweave VIM plugin: `<https://github.com/naught101/vim-pweave>`__ .

Spyder
------

Pweave can publish Spyder can scipts using ``#%%`` `code cell mark up <https://pythonhosted.org/spyder/editor.html#how-to-define-a-code-cell>`_ .
