


Using Pweave with Emacs
=======================

For me the best option for editing Pweave files is Emacs using the noweb-mode. I use .Pnw for Pweave documents written with reST markup and .Plw for LaTeX markup. Here is what I have in my ~/.emacs.d/init.el to make Emacs recognize my Pweave documents correctly. 

:: 

   ;Pnw-mode for Pweave reST documents
   (defun Pnw-mode ()
     	  (require 'noweb-font-lock-mode)
          (noweb-mode)
	  (setq noweb-default-code-mode 'python-mode)
          (setq noweb-doc-mode 'rst-mode))

   (setq auto-mode-alist (append (list (cons "\\.Pnw$" 'Pnw-mode))
		      auto-mode-alist))

   ;Plw-mode for Pweave Latex documents
   (defun Plw-mode ()
   	  (require 'noweb-font-lock-mode)
  	  (noweb-mode)
   	  (setq noweb-default-code-mode 'python-mode)
  	  (setq noweb-doc-mode 'latex-mode))
	  
   (setq auto-mode-alist (append (list (cons "\\.Plw$" 'Plw-mode))
		      auto-mode-alist))


The code simply sets the documenation mode (*noweb-doc-mode as rst-mode*) as reStructuredText or LaTeX depending on the extension and the code mode as Python, so that the code chunks will be correctly formatted.

You can get the needed .el files and my full init.el from bitbucket: http://bitbucket.org/mpastell/emacs.d/src 
