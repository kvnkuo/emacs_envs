# emacs_envs
Configuring emacs for various development environments

## install el-get
Make sure git is installed.   
Run the following in emacs buffer(copy=paste to scratch buffer, C-j to run it) to initialize the installation

    (url-retrieve
      "https://raw.githubusercontent.com/dimitri/el-get/master/el-get-install.el"
      (lambda (s)
        (goto-char (point-max))
        (eval-print-last-sexp)))

Then, Use 

    M-x el-get-install   
    package: el-get

to install el-get package. The package will be installed in ~/.emacs.d/el-get/el-get


## Create init.el file in ~/.emacs.d directory
Simple init.el which will initializa el-get package

    (add-to-list 'load-path "~/.emacs.d/el-get/el-get")
    (require 'el-get)
    (add-to-list 'package-archives
      '("melpa" . "https://melpa.org/packages/"))
    (el-get 'sync)
    (package-initialize)

## General customization
The following customizations can be appended to the init.el one by one.   
Hide menu bar

    ;; hide menu bar
    (menu-bar-mode -1)

No backup files   

    ;; Prevent Emacs from making backup files
    (setq make-backup-files nil)

Change key binding of set-mark-command to ESC-SPC(from C-SPC)

    ;; change binding of C-SPC 'set-mark-command
    (global-set-key (kbd "M-SPC") 'set-mark-command)

## yaml-mode
To install yaml-mode

    M-x el-get-install   
    package: yaml-mode

To activate in init.el

    ;; enable yaml-mode
    (require 'yaml-mode)
    (add-to-list 'auto-mode-alist '("\\.yml$" . yaml-mode))
    (add-to-list 'auto-mode-alist '("\\.yaml$" . yaml-mode))
    
Optionally bind C-m to newline-and-indent

    ;; bind C-m to newline-and-indent
    (add-hook 'yaml-mode-hook
      '(lambda ()
        (define-key yaml-mode-map "\C-m" 'newline-and-indent)))

## Reference
* https://github.com/dimitri/el-get
* https://github.com/yoshiki/yaml-mode
