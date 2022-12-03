# Modus themes for GNU Emacs (Modus Operandi and Modus Vivendi)

A pair of highly accessible themes that conform with the WCAG AAA
standard for colour contrast between background and foreground
combinations (a minimum contrast of 7:1---the highest standard of its
kind).  The Modus themes also strive to empower users with red-green
color deficiency: this is achieved through customisation options that
replace all relevant instances of green with blue, as well as the
overall design of the themes which relies mostly on colours that cover
the blue-cyan-magenta side of the spectrum.

The themes are built into GNU Emacs 28 (development target).  They are
also distributed in several packages formats.

+ `modus-operandi` is light.
+ `modus-vivendi` is dark.

For some demo content, check:

+ The screenshots of the themes <https://protesilaos.com/emacs/modus-themes-pictures/>.
+ My videos on Emacs <https://protesilaos.com/code-casts/>.

Sources:

+ Package name (GNU ELPA): `modus-themes` (also built into Emacs >= 28)
+ Official manual: <https://protesilaos.com/emacs/modus-themes>
+ Change log: <https://protesilaos.com/emacs/modus-themes-changelog>
+ Colour palette: <https://protesilaos.com/emacs/modus-themes-colors>
+ Git repo on SourceHut: <https://git.sr.ht/~protesilaos/modus-themes>
  - Mirrors:
    + GitHub: <https://github.com/protesilaos/modus-themes>
    + GitLab: <https://gitlab.com/protesilaos/modus-themes>
+ Mailing list: <https://lists.sr.ht/~protesilaos/modus-themes>
+ Backronym: My Old Display Unexpectedly Sharpened ... themes

## Quick setup for the latest version

### Built-in version

For the themes that are built into Emacs you cannot `require` the
package.  Use the following instead.

With `use-package`:

```elisp
(use-package emacs
  :init
  ;; Add all your customizations prior to loading the themes
  (setq modus-themes-italic-constructs t
        modus-themes-bold-constructs nil
        modus-themes-region '(bg-only no-extend))
  :config
  ;; Load the theme of your choice:
  (load-theme 'modus-operandi) ;; OR (load-theme 'modus-vivendi)
  :bind ("<f5>" . modus-themes-toggle))
```

Without `use-package`:

```elisp
;; Add all your customizations prior to loading the themes
(setq modus-themes-italic-constructs t
      modus-themes-bold-constructs nil
      modus-themes-region '(bg-only no-extend))

;; Load the theme of your choice:
(load-theme 'modus-operandi) ;; OR (load-theme 'modus-vivendi)

(define-key global-map (kbd "<f5>") #'modus-themes-toggle)
```

### Packaged version

With `use-package`:

```elisp
(use-package modus-themes
  :ensure
  :init
  ;; Add all your customizations prior to loading the themes
  (setq modus-themes-italic-constructs t
        modus-themes-bold-constructs nil
        modus-themes-region '(bg-only no-extend))

  ;; Load the theme files before enabling a theme
  (modus-themes-load-themes)
  :config
  ;; Load the theme of your choice:
  (modus-themes-load-operandi) ;; OR (modus-themes-load-vivendi)
  :bind ("<f5>" . modus-themes-toggle))
```

Without `use-package`:

```elisp
(require 'modus-themes)

;; Add all your customizations prior to loading the themes
(setq modus-themes-italic-constructs t
      modus-themes-bold-constructs nil
      modus-themes-region '(bg-only no-extend))

;; Load the theme files before enabling a theme
(modus-themes-load-themes)

;; Load the theme of your choice:
(modus-themes-load-operandi) ;; OR (modus-themes-load-vivendi)

(define-key global-map (kbd "<f5>") #'modus-themes-toggle)
```

Note: make sure that you **do not customise** `custom-theme-load-path`
or `custom-theme-directory` _after_ the themes' package declaration.
That will lead to failures in loading the files.  If you must change
those variables, do it before the package declaration.

## All customisations in short

While you should read the manual for all the details (see next section),
here is a snippet with all current customisation options and their
possible values.  Note that those settings are only for purposes of
demonstration:

```elisp
(setq modus-themes-italic-constructs t
      modus-themes-bold-constructs nil
      modus-themes-mixed-fonts nil
      modus-themes-subtle-line-numbers nil
      modus-themes-deuteranopia t
      modus-themes-variable-pitch-ui nil

      modus-themes-fringes nil ; {nil,'subtle,'intense}

      ;; Options for `modus-themes-mode-line' are either nil, or a list
      ;; that can combine any of `3d' OR `moody', `borderless',
      ;; `accented', a natural number for extra padding (or a cons cell
      ;; of padding and NATNUM), and a floating point for the height of
      ;; the text relative to the base font size (or a cons cell of
      ;; height and FLOAT)
      modus-themes-mode-line '(accented borderless (padding . 4) (height . 0.9))

      ;; Same as above:
      ;; modus-themes-mode-line '(accented borderless 4 0.9)

      ;; Options for `modus-themes-links' are either nil (the
      ;; default), or a list of properties that may include any of
      ;; those symbols: `neutral-underline' OR `no-underline', `bold',
      ;; `italic'.
      modus-themes-links '(neutral-underline)

      ;; Options for `modus-themes-prompts' are either nil (the
      ;; default), or a list of properties that may include any of those
      ;; symbols: `background', `bold', `italic'.
      modus-themes-prompts '(italic bold)

      ;; The `modus-themes-completions' is an alist that reads three
      ;; keys: `matches', `selection', `popup'.  Each accepts a nil
      ;; value (or empty list) or a list of properties that can include
      ;; any of the following (for WEIGHT read further below):
      ;;
      ;; `matches' - `background', `intense', `underline', `italic', WEIGHT
      ;; `selection' - `accented', `intense', `underline', `italic', `text-also' WEIGHT
      ;; `popup' - same as `selected'
      ;; `t' - applies to any key not explicitly referenced (check docs)
      ;;
      ;; WEIGHT is a symbol such as `semibold', `light', or anything
      ;; covered in `modus-themes-weights'.  Bold is used in the absence
      ;; of an explicit WEIGHT.
      modus-themes-completions '((matches . (extrabold))
                                 (selection . (semibold accented))
                                 (popup . (accented intense)))

      ;; Options for `modus-themes-region' are either nil (the default),
      ;; or a list of properties that may include any of those symbols:
      ;; `no-extend', `bg-only', `accented'
      modus-themes-region '(bg-only no-extend)

      modus-themes-org-blocks 'gray-background ; {nil,'gray-background,'tinted-background}

      modus-themes-headings ; this is an alist: read the manual or its doc string
      '((1 . (variable-pitch 1.3))
        (2 . (rainbow 1.1))
        (t . (semibold))))
```

## Further information

Read the [Info manual HTML](https://protesilaos.com/emacs/modus-themes)
version for how to install, load, enable, and customise the themes.  If
you are using the latest version of the themes, you already have the
manual installed: evaluate `(info "(modus-themes) Top")` to start
reading it.

The themes cover a broad range of packages and are highly customisable.
