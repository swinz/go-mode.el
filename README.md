This is go-mode, the Emacs mode for editing Go code.

It is a complete rewrite of the go-mode that shipped with Go 1.0.3 and
before, and was part of Go 1.1 until Go 1.3. Beginning with Go 1.4,
editor integration will not be part of the Go distribution anymore,
making this repository the canonical place for go-mode.


# Features

In addition to normal features, such as fontification and indentation,
and close integration with familiar Emacs functionality (for example
syntax-based navigation like `beginning-of-defun`), go-mode comes with
the following extra features to provide an improved experience:

- Integration with `gofmt` by providing a command of the same name,
  and `gofmt-before-save`, which can be used in a hook to format Go
  buffers before saving them.
  - Setting the `gofmt-command` variable also allows using
    `goimports`.
- Integration with `godoc` via the functions `godoc` and
  `godoc-at-point`.
- Integration with the Playground
  - `go-play-buffer` and `go-play-region` to send code to the
    Playground
  - `go-download-play` to download a Playground entry into a new
    buffer
- Managing imports
  - A function for jumping to the file's imports (`go-goto-imports` -
    `C-c C-g i`)
  - A function for adding imports, including tab completion
    (`go-import-add`, bound to `C-c C-a`)
  - A function for removing or commenting unused imports
    (`go-remove-unused-imports`)
- Integration with godef
  - `godef-describe` (`C-c C-d`) to describe expressions
  - `godef-jump` (`C-c C-j`) and `godef-jump-other-window` (`C-x 4 C-c
    C-j`) to jump to declarations
  - This requires you to install godef via `go get
  github.com/rogpeppe/godef`.
- Basic support for imenu (functions and variables)
- Built-in support for displaying code coverage as calculated by `go
  test` (`go-coverage`)
- Several functions for jumping to and manipulating the individual
  parts of function signatures. These functions support anonymous
  functions, but are smart enough to skip them when required (e.g.
  when jumping to a method receiver or docstring.)
  - Jump to the argument list (`go-goto-arguments` - `C-c C-g a`)
  - Jump to the docstring, create it if it does not exist yet
    (`go-goto-docstring` - `C-c C-g d`).
  - Jump to the function keyword (`go-goto-function` - `C-c C-g f`)
  - Jump to the function name (`go-goto-function-name` - `C-c C-g n`)
  - Jump to the return values (`go-goto-return-value` - `C-c C-g r`)
  - Jump to the method receiver, adding a pair of parentheses if no
    method receiver exists (`go-goto-method-receiver` - `C-c C-g m`).

  All of these functions accept a prefix argument (`C-u`), causing
  them to skip anonymous functions.

# Installation

## MELPA

The recommended way of installing go-mode is via
[ELPA](http://www.emacswiki.org/emacs/ELPA), the Emacs package
manager, and the
[MELPA repository](http://melpa.org/#/getting-started), which provides
an up-to-date version of go-mode.

If you're not familiar with ELPA yet, consider reading
[this guide](http://ergoemacs.org/emacs/emacs_package_system.html).

## Manual

To install go-mode manually, place `go-mode.el` and
`go-mode-autoloads.el` in a directory of your choice, add it to your
load path and require `'go-mode-autoloads`:

    (add-to-list 'load-path "/place/where/you/put/it/")
    (require 'go-mode-autoloads)

Either evaluate both statements with `C-x C-e`, or restart Emacs.

As a side note, normally the autoloads file shouldn't be part of the
package, as it's supposed to be automatically generated by ELPA, or
manually by the user with `update-file-autoloads`. go-mode includes
said file because it used to when it was part of the Go distribution
and this makes upgrading easier for some people.

# Other extensions

There are several third party extensions that can enhance the Go
experience in Emacs.

## Syntax/error checking

There are two ways of using flymake with Go:

1. [goflymake](https://github.com/dougm/goflymake), which internally
uses `go build` to capture all errors that a regular compilation would
also produce
2. [flymake-go](http://marmalade-repo.org/packages/flymake-go) for a
more lightweight solution that only uses `gofmt` and as such is only
able to catch syntax errors. Unlike goflymake, however, it does not
require an additional executable.

Additionally, there is
[flycheck](https://github.com/flycheck/flycheck), a modern replacement
for flymake, which comes with built-in support for Go. In addition to
using `go build` or `gofmt`, it also has support for `go vet`,
`golint` and `errcheck`.

## Auto completion

For auto completion, take a look at
[gocode](https://github.com/nsf/gocode).

## eldoc

https://github.com/syohex/emacs-go-eldoc provides eldoc functionality
for go-mode.

## Snippets

I maintain a set of YASnippet snippets for go-mode at
https://github.com/dominikh/yasnippet-go

## Integration with errcheck

https://github.com/dominikh/go-errcheck.el provides integration with
[errcheck](https://github.com/kisielk/errcheck).

# Donations

I am accepting donations for go-mode, but it has to be said that even
though I am its primary developer, there are several third party
contributions with varying complexity. Donations would be towards me,
Dominik Honnef, and not go-mode as a whole.

<a href='http://www.pledgie.com/campaigns/21377'><img alt='Click here to lend your support to: go-mode.el and make a donation at www.pledgie.com !' src='http://www.pledgie.com/campaigns/21377.png?skin_name=chrome' border='0' /></a>
