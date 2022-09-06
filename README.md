# hg-number

A Python 3.6 wrapper script around `hg` that does for `hg` what
[git-number](https://github.com/holygeek/git-number) does for `git`.

No installation required. Simply add to your `$PATH`.

If you like, you can add some convenient aliases to your `.bashrc`

```shell
alias hn=hg-number
alias vn='hg-number -c vi'
```

Where `g4 status` shows output like

```shell
$ hg status
M contrib/fuzz/xdiff.cc
A contrib/acme.py
M thirdparty/xdiff/xprepare.c
```

`hn` shows paths relative to the current working directory prefixed by a
shortcut, eg, from `contrib` this shows:

```shell
$ hn

1 M fuzz/xdiff.cc
2 A acme.py
3 M ../thirdparty/xdiff/xprepare.c
```

`hn status` stores a list of shortcuts and the repo-relative paths they map onto in
`.hg/hg-number-shortcuts.txt`.

When `hn` is run with arguments, it expands any shortcuts to full depot paths
and invokes `hg` with these arguments.

In addition, if the first argument to `hn` is `-c`, the second argument is
treated as the shell command to run, and the shortcuts are expanded to paths
relative to the current directory.

`hn revert 3` expands to `hg revert ../thirdparty/xdiff/xprepare.c`

`hn -c wc -l 1-3` expands to `wc -l fuzz/xdiff.cc acme.py ../thirdparty/xdiff/xprepare.c`
