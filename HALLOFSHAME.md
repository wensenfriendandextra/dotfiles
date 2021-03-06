# Homedir Hall of Shame

Here are a list of projects that insist on living in the home directory and
whose dotfiles or dotdirs are either hard or impossible to move or factor.

## TL;DR / Table of Shames

Shame on them:

* [CUPS](#cups)
* [Dropbox](#dropbox)
* [ghci](#ghci)
* [gist](#gist)
* [Heroku toolbelt](#heroku-toolbelt)
* [Keybase installer](#keybase-installer)
* [matplotlib](#matplotlib)
* [mutt](#mutt)
* [GNU Parallel](#gnu-parallel)
* [PyPI](#pypi)
* [RubyGems](#rubygems)
* [Shout](#shout)
* [tox](#tox)
* [Travis client](#travis-client)
* [tmux](#tmux)

## Reasonable

There are large and crucial projects that somewhat deserve a space in
`HOME`. The "reasonable" list also includes projects that install binaries to
`HOME`, e.g., Linuxbrew, and various version managers.

* Shells:

  * Bash;
  * Zsh (including `.zprezto`).

* Editors:

  * Atom;
  * Emacs.

* Version managers:

  * pyenv;
  * RVM.

* Misc:

  * fontconfig;
  * GnuPG;
  * Linuxbrew;
  * SSH;
  * Vagrant.

## Shameful

These projects should feel ashamed by their lack of customizability and
pollution to user home.

### CUPS

See the `FILES` section of `man 1 cups`: `~/.cups/client.conf` and
`~/.cups/lpoptions`.

### Dropbox

Okay, Dropbox is used by hundreds of millions of dummies so I won't expect
customizability on this front, but can't you move `~/.dropbox` to
`~/Library/Caches`?

### ghci

Ticket: [GHC#6077](https://ghc.haskell.org/trac/ghc/ticket/6077).

### gist

By `gist` we mean [defunkt/gist](https://github.com/defunkt/gist).

Worst offender ever. It stores the OAuth token in `~/.gist`, making even
symlinking impractical.

Related PR: [`defunkt/gist#189`](https://github.com/defunkt/gist/pull/189).

Full solution: use my enhanced fork!
[`zmwangx/gist`](https://github.com/zmwangx/gist), now also on
[RubyGems.org](https://rubygems.org/gems/gistl):

```
gem install gistl
```

Gemfile:

```ruby
gem 'gistl', :require => 'gist'
```

### Heroku toolbelt

Issue: [`heroku/toolbelt#115`](https://github.com/heroku/toolbelt/issues/115).

### Keybase installer

Issue:
[`keybase/node-installer#65`](https://github.com/keybase/node-installer/issues/65).

### matplotlib

According to the
[FAQ](http://matplotlib.org/faq/environment_variables_faq.html#envvar-MPLCONFIGDIR),
matplotlib puts its config as well as caches in a single directory,
`MPLCONFIGDIR`, which is far from XDG conformant. Fortunately I rarely use
matplotlib and don't have any personal customizations, so the directory is
simply dropped to `$XDG_CACHE_HOME/matplotlib` (see `env/env.d/matplotlib`).

### mutt

See the `FILES` section of `man 1 mutt`: either `~/.muttrc` or
`~/.mutt/muttrc`.

### GNU Parallel

`$ENV{'HOME'} . "/.parallel/foo"` appears everywhere in source code.

### PyPI

According to
[the docs](https://docs.python.org/3/distutils/packageindex.html#pypirc), the
path of the config file has to be `~/.pypirc`.

### RubyGems

`~/.gem/credentials` is hard-coded in
[source code](https://github.com/rubygems/rubygems/blob/503556f/lib/rubygems/config_file.rb#L274-L276).

### Shout

`path.resolve(this.HOME) + "/config"` is hard-coded in
[source code](https://github.com/erming/shout/blob/master/src/helper.js).

### tox

tox has no global configuration file, and unless one enforces one's own
preferences for `distshare` on other developers by setting `distshare` in
`tox.ini`, it defaults to `{homedir}/.tox/distshare`. See
[docs](http://codespeak.net/tox/config.html). (And the stupid thing is, I don't
really need to access build artifects between runs. I guess `~/.tox/distshare`
— serving no purpose at all in my case — has to be routinely wiped.)

### Travis client

Issue:
[`travis-ci/travis.rb#219`](https://github.com/travis-ci/travis.rb/issues/219).

### tmux

See the `FILEs` section of `man 1 tmux`: `~/.tmux.conf`.
