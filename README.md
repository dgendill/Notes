# Dom's Notes

A collection of notes in org-mode format.

#+RESULTS: TableOfContents
: 
: - [How To Install Node.js For Personal (Non-Server) Use](../blob/master/howto/install-nodejs.org)
: - [How to Remap Right Menu Key to Ctrl In Linux](../blob/master/howto/remap-right-menu-key-to-ctrl.org)


## Export File To HTML

`M-x org-html-export-to-html`

## Export File To ASCII

`M-x org-html-export-to-ascii`

http://orgmode.org/worg/dev/org-element-api.html#attributes
https://github.com/caiorss/Emacs-Elisp-Programming#defining-functions
https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#links
http://orgmode.org/manual/Code-evaluation-security.html#Code-evaluation-security
http://orgmode.org/manual/Working-With-Source-Code.html#Working-With-Source-Code

```elisp
#+begin_src emacs-lisp :exports none
   (org-babel-do-load-languages
    'org-babel-load-languages
    '((python . t) (js . t))
#+end_src

#+NAME: TableOfContents
#+begin_src elisp :results output
  (defun getFilesInDir (dir)
    "Show the files in the folder that are registered with git."
    (split-string
     (shell-command-to-string
      (concat "git ls-files " dir)) "\n" t))

  (defun getDocumentTitle ()
    "Assumes that an org-mode buffer is open."
    (org-element-map (org-element-parse-buffer) 'keyword
        (lambda (np) (
            ;; print (org-element-property :key np)
            if (equal (org-element-property :key np) "TITLE")
                (org-element-property :value np)
                nil))))

  (defun fileToMarkdownLink (file)
    (with-temp-buffer
      (insert-file-contents file)
      (org-mode)
      (concat "\n- [" (nth 0 (getDocumentTitle)) "](" file ")")))

  (dolist
    (link (mapcar 'fileToMarkdownLink (getFilesInDir "howto")))
    (princ link))
#+end_src

```
