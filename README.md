<h1 align="center">pure bash</h1> <p align="center">A [WIP] collection of
pure bash alternatives to external processes.</p>

The goal of this repository is to document known and unknown methods of
doing various tasks using only built-in bash features. Using the snippets
from this guide can help to remove unneeded dependencies from your scripts
and in most cases make them that little bit faster. I came across these
tips and discovered a few while developing
[neofetch](https://github.com/dylanaraps/neofetch),
[pxltrm](https://github.com/dylanaraps/pxltrm) and some other smaller
projects.

This repository is open to contribution. If you see something that is
incorrectly described, buggy or outright wrong, open an issue or send a
pull request. If you know a handy snippet that is not included in this
list, send a pull request!


## Table of Contents

<!-- vim-markdown-toc GFM -->

* [Getting the terminal size (*in a script*).](#getting-the-terminal-size-in-a-script)
* [Get the current date using `strftime`.](#get-the-current-date-using-strftime)
* [Get the directory name of a file path.](#get-the-directory-name-of-a-file-path)
* [Convert a hex color to RGB](#convert-a-hex-color-to-rgb)
* [Convert an RGB color to hex.](#convert-an-rgb-color-to-hex)

<!-- vim-markdown-toc -->


## Getting the terminal size (*in a script*).

This is handy when writing scripts in pure bash and `stty`/`tput` can’t be
called.

```sh
get_term_size() {
    # Usage: get_term_size

    # (:;:) is a micro sleep to ensure the variables are
    # exported immediately.
    shopt -s checkwinsize; (:;:)
    printf '%s\n' "$LINES $COLUMNS"
}
```


## Get the current date using `strftime`.

Bash’s `printf` has a built-in method of getting the date which we can use
in place of the `date` command in a lot of cases.

**NOTE:** Requires `bash` 4+

```sh
date() {
    # Usage: date "format"
    # See: 'man strftime' for format.
    printf "%($1)T\\n"
}
```

## Get the directory name of a file path.

Alternative to the `dirname` command.

```sh
dirname() {
    # Usage: dirname "path"
    printf ‘%s\n’ "${1%/*}/"
}
```

## Convert a hex color to RGB

```sh
hex_to_rgb() {
    # Usage: hex_to_rgb "#FFFFFF"
    ((r=16#${1:1:2}))
    ((g=16#${1:3:2}))
    ((b=16#${1:5:6}))

    printf '%s\n' "$r $g $b"
}
```

## Convert an RGB color to hex.

```sh
rgb_to_hex() {
    # Usage: rgb_to_hex "r" "g" "b"
    printf '#%02x%02x%02x\n' "$1" "$2" "$3"
}
```

