---
title: Using one bpython with multiple virtual environments
author: Alex
type: posts
date: 2024-09-29T20:49:33+02:00
url: /posts/bpython-with-multiple-virtual-environments/
categories:
    - Tutorial
tags:
    - Python
    - TIL
    - venv
    - REPL
---

I finally realized that I should change the default Python REPL. There are many REPLs that offer a much better experience—[ipython](https://ipython.org/), [bpython](https://bpython-interpreter.org/), and [ptpython](https://github.com/prompt-toolkit/ptpython) are probably the most well-known. In the past, I used ipython because I worked on many projects that involved Jupyter notebooks, so it came essentially for free whenever I installed the necessary packages.

However, in recent years, I've been working on a lot of projects that don't rely on Jupyter, meaning ipython wasn’t installed by default. This meant I always had to manually install it in any virtual environment where I wanted to use it—which I didn’t like, as I prefer to keep only project-specific dependencies in a virtual environment.

As a result, I relied on the plain old `python` REPL, with all its shortcomings—especially the difficulty of pasting code snippets (which, thankfully, will be improved with [Python 3.13](https://docs.python.org/3.13/whatsnew/3.13.html#whatsnew313-better-interactive-interpreter)).

Today, I started wondering if there was a way to use a REPL like `bpython` in every environment I have. You can install it once with [`pipx`](https://github.com/pypa/pipx) and use it everywhere, but it won't find any packages by default. While searching online, I came across a promising post on [Stack Overflow](https://stackoverflow.com/a/22182421). Although the post was from 2014 and the exact approach didn't work, with a bit of fiddling, I found a solution that seems to work. I added the following function to my `.zshrc`:


```zsh
function bp() {
    if test -n "$VIRTUAL_ENV"
    then
        PP=".$(python -c 'import sys; print(":".join(sys.path))')" 
        PYTHONPATH=${PP} bpython "$@"
    else
        bpython "$@"
    fi
}
```

Now, I can simply type  `bp`, and it will either start `bpython` directly or, if a virtual environment is active, it will set the `PYTHONPATH` to include the venv directory before starting the REPL.
