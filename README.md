TMUXIFY
=======

`tmuxify` is a bash tool inspired in [tmuxinator](https://github.com/tmuxinator/tmuxinator). The big difference is that it doesn't need Ruby.

### TL;DR

Fire up `tmux` with all the windows, panes and commands you need to start hacking at once!
You will need to create a `.tmuxify.layout` file in the root of your project and run `tmuxify`.

### The `.tmuxify.layout` file

Each line of this file tells `tmuxify` what to run, in what window and pane. It uses the following format

    window-name pane-number command

Yes, separated by a single space. Everything after the `pane-number` will be treated as part of the `command`.

Say I need two windows, one for `git` and one for `vim`, then my `.tmuxify.layout` file would look like:

    git 1 git pull
    vim 1 vim

Now I want the `git` window to have a pane with a `rack` server running.

    git 1 git pull
    git 2 rackup -p 8080
    vim 1 vim

Get the idea? Go crazy.

You can also select which pane will have focus after attaching the session by adding a `*` after the `pane-number`

    git 1* git pull
    git 2 rackup -p 8080
    vim 1 vim

### Caveats

1. The `.tmuxify.layout` file will need a `pane-number` even if the window has only one, like the `vim` example up there.
2. All the `commands` will `cd` to the directory where the `.tmuxify.layout` file is in.
3. The pane layout is always tiled.
4. The specified window names in the layout create new windows, so the first one is never used. Closing the first window will not renumber the existing ones. To fix that, add the following option in `~/.tmux.conf`

        set-option -g renumber-windows on

### Installation

With Homebrew

```shell
brew tap tonchis/goodies && brew install tmuxify
```

Or standalone. Here's a oneliner.

```shell
$ wget https://raw.githubusercontent.com/tonchis/tmuxify/master/bin/tmuxify && chmod +x tmuxify && sudo mv tmuxify /usr/local/bin
```

### Why?

I love `tmux` and the automation that `tmuxinator` offers to speed up my development, yet I find that needing Ruby and YAML is a bit cumbersome, given the powerful CLI tools that `tmux` offers.

### Thanks

To [inkel](https://github.com/inkel) and [djanowski](https://github.com/djanowski) for all their feedback :D
