# BeforeCommit

[![Build Status](https://travis-ci.org/EnvironmentAgency/before_commit.svg?branch=master)](https://travis-ci.org/EnvironmentAgency/before_commit)

A utility to provide a common set of definitions for code quality utilities
(for example, overcommit, rubocop, scss_lint and brakeman) across multiple
projects.

After installation, running `rake before_commit:run` will copy configuration
files to the current location, and install the code quality utilities.

If the configuration files need to be changed, the gem will be updated and
can be run again - installing the new configuration.

On cloning an application using BeforeCommit, you should run
`rake before_commit:run` before committing any new code to the repository.

## Configuration

This app is configured to install the `overcommit` gem, together with other
gems defined in `source/.overcommit_gems.rb` and to install a common set
of configuration files defined in the `source` folder.

If you want to use an alternative configuration, please feel free to fork
your own copy of this application, and modify the configuration to suit.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'before_commit'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install before_commit

## Usage

BeforeCommit adds a rake task `before_commit:run` to the host environment.

Running the following command

    rake before_commit:run

Will:
- run a set of checks (if specified) and exit unless the checks pass
- copy files from the gem into the current location
- run a set of commands

### Outside Rails

If you want to use this gem in a standalone ruby app or gem, add this to
that app or gem's Rakefile:

```ruby
require 'before_commit'
spec = Gem::Specification.find_by_name 'before_commit'
load "#{spec.gem_dir}/lib/tasks/before_commit.rake"
```

Note that if bin/rails is not detected, the brakeman test will be skipped.
However, as there isn't a way to skip in overcommit, brakeman shows as PASSED
even though the test has not run. 

### Checks

The checks are defined in `config/config.yml`. If the command defined in a
check returns an error, or if the output does not match the regular expression
defined as 'expected', the check will fail. If there was an error, the error
output will be displayed. If the expected match fails, the 'failure_message'
will be displayed.

### Files copied

After any checks have been successfully run, the files in the `source` folder
will be copied to the current location.

### Commands

The next step is for the commands defined in `commands` section of
`config/config.yml` to be run. For example:

    commands:
      - ls
      - "ruby -v"

Would cause the contents of the current directory to be listed, and the ruby
version to be displayed.

## Development

After checking out the repo, run `bin/setup` to install dependencies.
Then, run `rake test` to run the tests. You can also run `bin/console`
for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`.
To release a new version, update the version number in `version.rb`, and then
run `bundle exec rake release`, which will create a git tag for the version,
push git commits and tags, and push the `.gem` file
to [rubygems.org](https://rubygems.org).

## Contributing to this project

If you have an idea you'd like to contribute please log an issue.

All contributions should be submitted via a pull request.

## License

THIS INFORMATION IS LICENSED UNDER THE CONDITIONS OF THE OPEN GOVERNMENT LICENCE found at:

http://www.nationalarchives.gov.uk/doc/open-government-licence/version/3

The following attribution statement MUST be cited in your products and applications when using this information.

> Contains public sector information licensed under the Open Government license v3

### About the license

The Open Government Licence (OGL) was developed by the Controller of Her Majesty's Stationery Office (HMSO) to enable information providers in the public sector to license the use and re-use of their information under a common open licence.

It is designed to encourage use and re-use of information freely and flexibly, with only a few conditions.
