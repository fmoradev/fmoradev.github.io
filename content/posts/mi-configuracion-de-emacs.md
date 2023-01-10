---
title: "Mi Configuración de Emacs en GNU/Linux"
date: 2023-01-04T18:00:15-03:00
tags: ["emacs"]
draft: false
---
## ¿Por qué uso Emacs?

[Emacs](https://www.gnu.org/software/emacs/) es uno de los mejores editores de texto que conozco, aunque lo de *editor de texto* queda muy corto. Con **Emacs** puedes hacer prácticamente de todo lo que imagines. **Emacs** puede ser tu navegador web, tu IDE para programar, tu herramienta de control de tiempo, una aplicacion de To-Do, un reproductor de música, tu sistema operativo(sí, tu sistema operativo). **Emacs** es parte del proyecto [GNU](https://www.gnu.org/ "GNU") desarrollado en 1975 por [Richard Stallman](https://es.wikipedia.org/wiki/Richard_Stallman "Richard Stallman"), en un principio fue un interprete de [LISP](https://es.wikipedia.org/wiki/Emacs_Lisp "LISP"), el cual, se ha ido nutriendo de un sin fin de nuevas caracteristicas a través de los años. Actualmente es considerado junto con [VIM](https://es.wikipedia.org/wiki/Vim "VIM") uno de los editores de texto más potentes que existen (aunque esto no significa sencillo de aprender).

Hace unos 5 años atrás comencé a usar **Emacs** como mi editor preferido para programar **PHP** en esos tiempos, pero no fue hasta que conocí [Org-Mode](https://orgmode.org/ "Org-Mode") donde me olvidé por completo de [Sublime Text](https://www.sublimetext.com/ "Sublime Text"). Ahora uso **Emacs** para programar en **Ruby On Rails**, **PHP**, **Javascript**, **Python** y como mi herramienta **GTD** para organizar mi vida, proyectos y que haceres.

Es por eso que a continuación te muestro mi configuración por si te ánimas a probar el mejor editor que existe[^1].

## Instalación

**Emacs** está desarrollado para sacar toda su potencia en sistemas operativos [GNU/Linux](https://www.gnu.org/gnu/linux-and-gnu.html "GNU/Linux"), aunque existen versiones para sistemas **Windows**, **MacOS** y **BSDs** veamos como instalar en cada uno:

### GNU/Linux

En el sistema del pingüino *emacs* se encuentra en los repositorios[^2] oficiales de cada distribución y lo único que debes tener en cuenta es la versión disponible en estos repositorios, por ejemplo para instalar en:

#### Archlinux

```bash
sudo pacman -S emacs
```

#### Debian y derivadas

```bash
sudo apt install emacs-gtk
```

#### Fedora

```bash
sudo dnf install emacs
```

#### Void Linux

```bash
sudo xbps-install emacs
```

### BSDs

#### FreeBSD

```bash
pkg install emacs-devel
```

### MacOS

#### Homebrew

```bash
brew cask install emacs
```

#### MacPorts

```bash
sudo port install emacs-app
```

### Windows

En windows basta descargar el ejecutable ```.exe``` desde un [GNU Mirror](http://ftpmirror.gnu.org/emacs/windows "Emacs Windows Download") y seguir el proceso de instalación.

## Configuración

Los archivos de configuración de **emacs** deben tener la extensión ```.el```(también pueden ser ```.org```) que es la extensión de archivos escritos en lenguaje de programación [LISP](https://es.wikipedia.org/wiki/Lisp) y se ubican dentro de la carpeta ```.emacs.d```, la cual, está oculta en tu directorio personal(fijate en el punto inicial). En windows esta carpeta se encuentra en la ruta ```C:\Users\username\AppData\Roaming```(aunque se puede configurar tu **HOME** con variables de entorno). El archivo de configuración principal en **emacs** es ```init.el``` y mantengo separados otros archivos en una carpeta  `config`. Ejemplo de mi estructura es como la siguiente:

```shell
.emacs.d (folder)
-- config (folder)
---- configemacs.el (setup emacs)
---- configorg.el (setup org-mode)
---- configdev.el (setup desarrollo)
-- init.el (archivo principal setea folder config)
-- custom.el (archivo autogenerado)
```

### init.el

Mi archivo **init.el** contiene el setup de repositorios para instalar aplicaciones en **Emacs**, repositorios como [GNU ELPA](https://elpa.gnu.org/ "GNU Emacs Lisp Package Archive"), [MELPA](https://melpa.org/ "Milkypostman’s Emacs Lisp Package Archive") y [Org-Mode](https://orgmode.org/elpa.html):

```lisp
(require 'package)
(add-to-list 'package-archives '("melpa" . "https://melpa.org/packages/") t)
(add-to-list 'package-archives '("org" . "https://orgmode.org/elpa/") t)
(package-initialize)
(add-to-list 'load-path "~/.emacs.d/config")
(load "configemacs.el")
(load "configdev.el")
(load "configorg.el")
(setq custom-file "~/.emacs.d/custom.el")
(load custom-file 'noerror)
```

### custom.el

El archivo **custom.el** contiene codigo autogenerado por **emacs** cada vez que seteas un valor a alguna de las innumerables variables que puedes modificar dentro de **emacs**, yo mantengo esto separado para llevar un orden y que mi **init.el** se mantenga limpio.

### config/configemacs.el

El archivo **configemacs.el** es donde seteo la configuración de **emacs**. Esto se refiere a configuración de letras, temas, modos, buffer y cualquier cosa que desee modificar.

```lisp
;; Configurar titulo de ventana
(setq-default frame-title-format "%b")

;; Configurar tipo letra por defecto
(add-to-list 'default-frame-alist '(font . "Jetbrains Mono Regular-10"))
(set-face-attribute 'default nil
                    :family "Jetbrains Mono Regular"
                    :height 100
                    :weight 'normal
                    :width 'normal)

;; Configurar theme
(load-theme 'nimbus t)

;; Quitar sonido campana error
(setq ring-bell-function 'ignore)

;; Recolector de basura
(setq gc-cons-threshold 50000000)
(setq large-file-warning-threshold 100000000)

;; Usuario
(setq user-full-name "Jhon Doe")
(setq user-email-address "algo@algo.com")

;; Muestra el reloj en formato 24 hrs
(setq display-time-24hr-format t) ; Muestra el reloj en formato 24 hrs
(setq display-time-format "%H:%M"); Le da formato H:M
(display-time) ; muestra el reloj

;; Deshabilita pantalla de inicio y muestra mensaje personalizado
(setq inhibit-startup-screen t)
(setq inhibit-startup-message t)
(setq initial-scratch-message ";; Happy Hacking")

;; Deshabilita backups, autoguardado y ficheros .#
(setq create-lockfiles nil)
(setq make-backup-files nil)
(setq auto-save-default nil)

;; Sustituye yes/no por y/n
(fset 'yes-or-no-p 'y-or-n-p)

;; Pantalla completa
(add-to-list 'default-frame-alist '(fullscreen . maximized))
(custom-set-variables '(initial-frame-alist (' ((fullscreen . maximized)))))

;; Seguir enlaces simbolicos
(setq vc-follow-symlinks t)

;; Muestra tamanios de archivo
(size-indication-mode t)

;; Deshabilita bar-mode y scroll-mode
(tool-bar-mode -1)
(toggle-scroll-bar -1)
(menu-bar-mode -1)

;; Deshabilita tooltips
(tooltip-mode -1)

;; Mejora scrolling
(setq scroll-margin 0)
(setq scroll-conservatively 100000)
(setq scroll-preserve-screen-position 1)

;; Muestra numero de fila y columna
(setq global-linum-mode t)
(global-visual-line-mode 1)
(global-display-line-numbers-mode)

;; Company-mode
(add-hook 'after-init-hook 'global-company-mode)

;; Mejoras de parentesis
(show-paren-mode 1);Muestra el parentesis padre
(add-hook 'prog-mode-hook #'rainbow-delimiters-mode);rainbow-delimiters

;; UTF-8
(set-terminal-coding-system 'utf-8)
(set-language-environment 'utf-8)
(set-keyboard-coding-system 'utf-8)
(prefer-coding-system 'utf-8)
(setq locale-coding-system 'utf-8)
(set-default-coding-systems 'utf-8)
(set-terminal-coding-system 'utf-8)

;; UNIX LF
(setq-default buffer-file-coding-system 'utf-8-unix)

;; Smartparens
(require 'smartparens-config)

;; Flycheck
(add-hook 'after-init-hook #'global-flycheck-mode)

;; Spaceline
(require 'spaceline-config)
(spaceline-emacs-theme)

;; Ivy y Counsel
(ivy-mode 1)
(global-set-key (kbd "C-s") 'swiper-isearch)
(global-set-key (kbd "M-x") 'counsel-M-x)
(global-set-key (kbd "C-x C-f") 'counsel-find-file)
(global-set-key (kbd "M-y") 'counsel-yank-pop)
(global-set-key (kbd "<f1> f") 'counsel-describe-function)
(global-set-key (kbd "<f1> v") 'counsel-describe-variable)
(global-set-key (kbd "<f1> l") 'counsel-find-library)
(global-set-key (kbd "<f2> i") 'counsel-info-lookup-symbol)
(global-set-key (kbd "<f2> u") 'counsel-unicode-char)
(global-set-key (kbd "<f2> j") 'counsel-set-variable)
(global-set-key (kbd "C-x b") 'ivy-switch-buffer)
(global-set-key (kbd "C-c v") 'ivy-push-view)
(global-set-key (kbd "C-c V") 'ivy-pop-view)
(global-set-key (kbd "C-c c") 'counsel-compile)
(global-set-key (kbd "C-c g") 'counsel-git)
(global-set-key (kbd "C-c j") 'counsel-git-grep)
(global-set-key (kbd "C-c L") 'counsel-git-log)
(global-set-key (kbd "C-c k") 'counsel-rg)
(global-set-key (kbd "C-c m") 'counsel-linux-app)
(global-set-key (kbd "C-c n") 'counsel-fzf)
(global-set-key (kbd "C-x l") 'counsel-locate)
(global-set-key (kbd "C-c J") 'counsel-file-jump)
(global-set-key (kbd "C-S-o") 'counsel-rhythmbox)
(global-set-key (kbd "C-c w") 'counsel-wmctrl)
(global-set-key (kbd "C-c C-r") 'ivy-resume)
(global-set-key (kbd "C-c b") 'counsel-bookmark)
(global-set-key (kbd "C-c d") 'counsel-descbinds)
(global-set-key (kbd "C-c g") 'counsel-git)
(global-set-key (kbd "C-c o") 'counsel-outline)
(global-set-key (kbd "C-c t") 'counsel-load-theme)
(global-set-key (kbd "C-c F") 'counsel-org-file)
```

### config/configdev.el

este archivo contiene mi configuración de **emacs** para desarrollo, principalmente **PHP**, **Python** y **Javascript**, **Markdown**, también uso **Magit** para trabajar con *git* sin salir del editor.

```lisp
;; Magit
(global-set-key (kbd "C-x g") 'magit-status)
(global-set-key (kbd "C-x M-g") 'magit-dispatch)
(global-set-key (kbd "C-c M-g") 'magit-file-dispatch)

;; Web Mode
(require 'web-mode)
(add-to-list 'auto-mode-alist '("\\.[agj]sp\\'" . web-mode))
(add-to-list 'auto-mode-alist '("\\.as[cp]x\\'" . web-mode))
(add-to-list 'auto-mode-alist '("\\.erb\\'" . web-mode))
(add-to-list 'auto-mode-alist '("\\.mustache\\'" . web-mode))
(add-to-list 'auto-mode-alist '("\\.djhtml\\'" . web-mode))
(add-to-list 'auto-mode-alist '("\\.html?\\'" . web-mode))

;; Javascript
(add-hook 'js-mode-hook 'js2-minor-mode)
(add-to-list 'interpreter-mode-alist '("node" . js2-mode))

;; Php
(autoload 'php-mode "php-mode" "Major mode for editing PHP code." t)
(add-to-list 'auto-mode-alist '("\\.phtml$'" . php-mode))
(add-to-list 'auto-mode-alist '("\\.tpl$'" . php-mode))
(add-to-list 'auto-mode-alist '("\\.php$" . php-mode))
(add-to-list 'auto-mode-alist '("\\.inc$" . php-mode))

;; Neotree
(require 'neotree)
(global-set-key [f8] 'neotree-toggle)
(setq neo-theme (if (display-graphic-p) 'icons 'arrow))

;; Markdown Mode
(autoload 'markdown-mode "markdown-mode" "Major mode for editing Markdown files" t)
(add-to-list 'auto-mode-alist '("\\.markdown\\'" . markdown-mode))
(add-to-list 'auto-mode-alist '("\\.md\\'" . markdown-mode))
(autoload 'gfm-mode "markdown-mode" "Major mode for editing GitHub Flavored Markdown files" t)
(add-to-list 'auto-mode-alist '("README\\.md\\'" . gfm-mode))

;; Elpy
(elpy-enable)
```

### config/configorg.el

Este es mi santo grial, aquí seteo mi flujo **Org-Mode** y **GTD**, la cual, me permite mantenerme organizado(en otro post explicaré esto).

```lisp
;; Habilita ORG
(require 'org)

;; Oculta */o_
(setq org-hide-emphasis-markers t)

;; org bullets
(require 'org-bullets)
(add-hook 'org-mode-hook (lambda () (org-bullets-mode 1)))

;; Mejora Bullets
(font-lock-add-keywords 'org-mode '(("^ +\\([-*]\\) "(0 (prog1 () (compose-region (match-beginning 1) (match-end 1) "•"))))))

;; Adapta texto a ventana
(add-hook 'org-mode-hook 'visual-line-mode)

;; Atajos de teclado
(global-set-key (kbd "C-c l") 'org-store-link)
(global-set-key (kbd "C-c a") 'org-agenda)
(global-set-key (kbd "C-c c") 'org-capture)

;; Indent mode
(add-hook 'org-mode-hook 'org-indent-mode)

;; Mejora SRC blocks en org-mode
(setq org-src-fontify-natively t)

;; Log done
(setq org-log-done t)

;; Agenda files
(setq org-agenda-files '("~/GTD/life.org" "~/GTD/tickler.org"))

;; Captura
(setq org-capture-templates '(("i" "INBOX" entry (file+headline "~/GTD/inbox.org" "INBOX") "** %i%?")
         ("p" "PROYECTO" entry (file+headline "~/GTD/projects.org" "PROYECTOS") "** %i%?")
         ("r" "REUNION" entry (file+headline "~/GTD/life.org" "REUNIONES") "** TODO %i%? \n SCHEDULED: %^T")
         ("s" "SEGUIMIENTO" entry (file+headline "~/GTD/tickler.org" "SEGUIMIENTOS") "** %i%? \n %^T")))

;; Refile
(setq org-refile-targets '(("~/GTD/life.org" :maxlevel . 5)
      ("~/GTD/inbox.org" :maxlevel . 5)
      ("~/GTD/someday.org" :maxlevel . 5)))

;;TO-DO Keywords
(setq org-todo-keywords '((sequence "WAITING(w)" "TODO(t)" "NEXT(n)" "|" "DONE(d)")))
(setq org-todo-keyword-faces '(
          ("TODO" :foreground "red" :weight bold)
          ("WAITING" :foreground "orange" :weight bold)
          ("NEXT" :foreground "yellow" :weight bold)
          ("DONE" :foreground "green" :weight bold)))

;;Etiquetas
(setq org-tag-persistent-alist '(
        (:startgroup . "Hardware")
        ("@phone" . ?p)("@kindle" . ?k)("@car" . ?c)
        (:endgroup)
        (:startgroup . "Software")
        ("@tfs" . ?t)("@email" . ?e)("@audacity" . ?a)("@git" . ?g)("@browser" . ?b)("@emacs" . ?E)("@shell" . ?s)("@msoffice" . ?w)("@libreoffice" . ?l)("@obs" . ?o)
        (:endgroup)))
(setq org-tag-faces '(
        ("@phone" :foreground "#edd3bb" :weight bold)
        ("@kindle" :foreground "#c6e2ff" :weight bold)
        ("@car" :foreground "#F0FFFF" :weight bold)
        ("@tfs" :foreground "#f8f5f3" :weight bold)
        ("@email" :foreground "#d4ab2d" :weight bold)
        ("@audacity" :foreground "#ebc7ff" :weight bold)
        ("@git" :foreground "#efd1d1" :weight bold)
        ("@browser" :foreground "#6445bc" :weight bold)
        ("@emacs" :foreground "#00ffff" :weight bold)
        ("@shell" :foreground "#1dacd6" :weight bold)
        ("@msoffice" :foreground "#fae7b5" :weight bold)
        ("@libreoffice" :foreground "#318ce7" :weight bold)
        ("@obs" :foreground "#dfff80" :weight bold)))

;;Archivar
(setq org-archive-location "~/GTD/archive_%s::datetree/")

;;Funciones propias
(defun life() "Abrir archivo principal gtd." (interactive)(find-file "~/GTD/life.org"))
(defun inbox() "Abrir archivo inbox." (interactive)(find-file "~/GTD/inbox.org"))
(defun someday() "Abrir archivo de ideas." (interactive)(find-file "~/GTD/someday.org"))
(defun projects() "Abrir archivo de proyectos." (interactive)(find-file "~/GTD/projects.org"))
```

Pues hasta aquí este post con mi configuración de **Emacs**, si te ha servido favor compartelo y si tienes alguna duda puedes contactarme en mis redes sociales y con gusto te ayudo.

Hasta la próxima..

[^1]: Esta es una opinión personal y puede que no estes de acuerdo conmigo.

[^2]: Siempre existe la opción de compilar desde los archivos fuentes, pero no es recomendable para alguien que no tiene experiencia en este proceso.
