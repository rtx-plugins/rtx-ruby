# rtx-ruby

[![Build Status](https://github.com/rtx-plugins/rtx-ruby/actions/workflows/ci.yml/badge.svg?branch=master)](https://github.com/rtx-plugins/rtx-ruby/actions/workflows/ci.yml?query=branch%3Amaster++)

Ruby plugin for [rtx](https://github.com/jdxcode/rtx) version manager

## Install

```
rtx plugin add ruby
```

Please make sure you have the required [system dependencies](https://github.com/rbenv/ruby-build/wiki#suggested-build-environment) installed before trying to install Ruby. It is also recommended that you [remove other ruby version managers before using rtx-ruby](#troubleshooting)

## Use

Check [rtx](https://github.com/jdxcode/rtx) readme for instructions on how to install & manage versions of Ruby.

When installing Ruby using `rtx install`, you can pass custom configure options with the [env vars supported by ruby-build](https://github.com/rbenv/ruby-build#custom-build-configuration).

Under the hood, rtx-ruby uses [ruby-build](https://github.com/rbenv/ruby-build) to build and install Ruby, check its [README](https://github.com/rbenv/ruby-build/blob/master/README.md) for more information about build options and the [troubleshooting](https://github.com/rbenv/ruby-build/wiki#troubleshooting) wiki section for any issues encountered during installation of ruby versions.

You may also apply custom patches before building with `RUBY_APPLY_PATCHES`, e.g.

```
RUBY_APPLY_PATCHES=$'dir/1.patch\n2.patch\nhttp://example.com/3.patch' rtx install ruby 2.4.1
RUBY_APPLY_PATCHES=$(curl -s https://raw.githubusercontent.com/rvm/rvm/master/patchsets/ruby/2.1.1/railsexpress) rtx install ruby 2.1.1
```

Running `rtx plugin-update ruby` will update rtx-ruby and ensure the latest versions of ruby are available to install. By default rtx-ruby uses the latest release of ruby-build, however instead you can choose your own branch/tag through the `RTX_RUBY_BUILD_VERSION` variable:

```
RTX_RUBY_BUILD_VERSION=master rtx install ruby 2.6.4
```

## Default gems

rtx-ruby can automatically install a set of default gems right after
installing a Ruby version. To enable this feature, provide a
`$HOME/.default-gems` file that lists one gem per line, for example:

```
bundler
pry
gem-ctags
```

You can specify a non-default location of this file by setting a `RTX_GEM_DEFAULT_PACKAGES_FILE` variable.

## Migrating from another Ruby version manager

### `.ruby-version` file

rtx uses the `.tool-versions` for auto-switching between software versions.
To ease migration, you can have it read an existing `.ruby-version` file to
find out what version of Ruby should be used.

## Troubleshooting

If you are moving to rtx-ruby from another Ruby version manager, it is recommended to completely uninstall the old Ruby version manager before installing rtx-ruby.

If you install rtx and rtx-ruby and it doesn't make `ruby` and `irb` available in your shell double check that you have installed rtx correctly. Make sure you have [system dependencies](https://github.com/rbenv/ruby-build/wiki#suggested-build-environment) installed BEFORE running `rtx install ruby <version>`. After installing a Ruby with rtx, run `type -a ruby` to see what rubies are currently on your `$PATH`. The rtx `ruby` shim should be listed first, if it is not rtx is not installed correctly.

Correct output from `type -a ruby` (rtx shim is first in the list):

```
ruby is /Users/someone/.local/share/rtx/installs/<RUBY_VERSION>/ruby
ruby is /usr/bin/ruby
```

Incorrect output `type -a ruby`:

```
ruby is /usr/bin/ruby
```
