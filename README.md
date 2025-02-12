# Bundler::Dependencies

![Test](https://github.com/dvandersluis/bundler-dependencies/actions/workflows/test.yml/badge.svg)
![Lint](https://github.com/dvandersluis/bundler-dependencies/actions/workflows/lint.yml/badge.svg)
[![Gem Version](https://badge.fury.io/rb/bundler-dependencies.svg)](https://badge.fury.io/rb/bundler-dependencies)

Bundler plugin to inspect dependencies of gems used by your project.

A project's `Gemfile.lock` shows some basic information about what gems are directly depended on by other gems, but this extension takes it a step further and enumerates the entire dependency tree of each gem being depended on. For instance, `rails` has 12 direct dependencies, but altogether installs **40** gems.

Each dependency is a potential point of failure, vulnerability, maintenance and *complexity* for a project, so the goal of `bundle dependencies` is to shed some light on what's being installed by what. This shouldn't stop you from installing gems that are useful to your project, but to be able to make an educated decision if a gem with 25 dependencies is a worthy tradeoff, for example.  

## Installation

Add this line to your application's Gemfile:

```sh
plugin 'bundler-dependencies'
```

And then execute:

```sh
$ bundle install
```

Alternately, you can install the plugin directly:

```sh
$ bundle plugin install bundler-dependencies
```

## Usage

```sh
bundler dependencies [command]
                     [--path=PATH]                  # Path to Gemfile.lock to scan
                     [-W, --without=one two three]  # Gems to ignore
                     [-R, --without-rails]          # Ignore all Rails gems
```

Requires a `Gemfile.lock` or `gems.locked` file to evaluate.

## Commands

**NOTE:** By default, `bundler dependencies` runs the `count` command.

### Getting Help

* `bundle dependencies help` to get an overview of all commands.
* `bundle dependencies help COMMAND` to get help for a specific command.

### Count

Check how many dependencies each gem in the Gemfile has (use the `--minimum N` switch to limit the output to gems with at least `N` dependencies):

```sh
bundle dependencies [count] [--minimum N] 
```

### Find

Find all the gems in the Gemfile that depend on a given gem (either directly or indirectly), as well as all the dependency paths for that gem:

```sh
bundle dependencies find GEM
```

Get just the number of dependent gems:

```sh
bundle dependencies find GEM --quiet
```

### Graph

See a graph of all dependencies:
```sh
bundle dependencies graph
```

See a graph of all dependencies for a specific gem:
```sh
bundle dependencies graph GEMNAME
```

### Command Options

The following options can be used with any command:

* `--path PATH`: User the Gemfile for the project at `PATH`, rather than the current project's Gemfile.
* `--without foo bar baz`/`-W foo bar baz`: Exclude the listed gems from the scan. Any uses either directly in your Gemfile or as dependencies will be excluded, and not be counted.
* `--without-rails`/`-R`: Quick option to exclude all 1st party Rails gems from the scan.

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/dvandersluis/bundler-dependencies.
