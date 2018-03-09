## Welcome to Pear

Pear is command line utility used while pairing to ensure that each programmer is reflected in the git commits. Pear is inspired by [Hitch](https://github.com/therubymug/hitch).

## Installing Pear

Please check out the releases page to get the latest binary for your system

https://github.com/hashrocket/go-pear/releases

Then copy that binary to a directory in your path.


## Using Pear
### Move into a git repo

Pear only works inside of a git repo.  If you are outside of a git repo, you'll see an error message that looks like this:

```
> pear
Pear only works in a git repository
```

### Changing Pairs

	$ pear chriserin derekparker

When prompted, enter the developer's full name. This changes the local git configuration (configuration per git repository).

### Checking Pairs

	$ pear

Pear with no arguments will let you know what programmers are configured with git.

### So you just want to work alone

	$ pear chriserin

Will change the git configuration to use just your id.

### To remove local pear configuration

	$ pear -u

This will unset local user configuration and fall back to the global configuration.

### So you like giving credit

	$ pear chriserin derekparker briandunn jackchristenson jonallured andrewdennis joshdavey

Will let you setup your git configuration to reflect all the programmers that have contributed to a commit.

## How Pear works

Pear works by changing your local git configuration, the configuration for a specific repository. Pear stores the full name of each developer in the ~/.pearrc so that a programmer will only be prompted once for his/her full name.

If your workflow or your organization's workflow requires that the git author and git committer for commits should differ, you can change the following environment variables:

	GIT_COMMITTER_NAME

and

	GIT_COMMITTER_EMAIL

These environment variables override the details provided by the git configuration. At Hashrocket, we use "Hashrocket Workstation" as the `GIT_COMMITTER_NAME` to provide a little bit more detail about where the commit is coming from.

## Github Integration

Github now has its own multiple committer attribute [feature](https://help.github.com/articles/creating-a-commit-with-multiple-authors/).  `pear` is configured as a default to work with this new Github feature.  When you use pear, it will insert the following line into the `prepare-commit-msg` hook.

``` sh
pear --augment-commit-message $1 $2 $3
```

That hook manipulates your commit message to include additional committers in this format:

```
Co-authored-by: Chris Erin <chris.erin@gmail.com>
```

You can toggle this feature on and off with the `pear --github-integration` or `pear -i` option:

``` sh
pear -i on
pear -i off
```

### About

[![Hashrocket logo](https://hashrocket.com/hashrocket_logo.svg)](https://hashrocket.com)

Pear is supported by the team at [Hashrocket, a multidisciplinary design and
development consultancy](https://hashrocket.com). If you'd like to [work with
us](https://hashrocket.com/contact-us/hire-us) or [join our
team](https://hashrocket.com/contact-us/jobs), don't hesitate to get in touch.
