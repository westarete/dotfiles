# Dot Files for West Arete

These are the common dot files that we share across our home directories.

As of yet, there is no fancy installation script; just manually put these in
place, or blend them with what you have now.

They're named here without the leading dot, so that the repository is easy to
work with. You'll need to rename them e.g. from `gemrc` to `~/.gemrc` when you
install them.

## Some handy binaries

`brew install vim` Ironically, the version of vim that ships with Mac OS X does
not integrate with the system clipboard. The Homebrew version does.

`brew install tmux` Tmux is like the next-generation replacement for screen. It
allows you to open split panes so that, for instance, you can have your vim
environment, rspec runner, and a ruby console, all open at the same time in the
same terminal window. It's also excellent for pairing.

`brew install the_silver_searcher` Blindingly-fast version of ack. Even if you
don't use the command, parts of the .vimrc contained in this repository depend on
it.

