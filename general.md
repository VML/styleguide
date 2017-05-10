# General

## Table of Contents

1. [Encryption and Protocol](#encryption-and-protocol)
1. [Fonts](#fonts)
1. [Indentation](indentation)
1. [Node](#node)
1. [Comments](#comments)
1. [General Formatting](#general-formatting)
   1. [Indentation](#indentation)
   1. [Whitespace](#whitespace)
   1. [Line Endings (Git)](#line-endings)

## Encryption and Protocol

Encrypt all network transfer and use the HTTPS protocol. The Protocol Relative URL pattern of omitting a protocol and allowing the browser to determine if a resource is encrypted is now [considered an anti-pattern](https://www.paulirish.com/2010/the-protocol-relative-url/).

```
<!-- Not Recommended -->
<link href="//fonts.googleapis.com/css?family=Roboto" rel="stylesheet">

<link href="http://fonts.googleapis.com/css?family=Roboto" rel="stylesheet">

<!-- Recommended -->
<link href="https://fonts.googleapis.com/css?family=Roboto" rel="stylesheet">
```

## Fonts

### Webfonts

In general it is best to load webfonts asynchronously. After a user has visited a page on the site once those fonts will usually be cached in the browser so they should only see a FOUT once. This downside of a single FOUT is usually outweighed by the benefits of a significantly faster loading site that is never blocked from loading if the resource, be it Google or Typekit, is unable to serve the fonts that have been requested.

## Node

### NPM

#### `.npmrc`

Installing NPM packages is great until members on a team aren't using the same versions. This is usually caused by a `^` or `~` in front of a package version in your package.json. This can be solved by an addition to the command line (more cognitive load) or a simple `.npmrc` file placed in the root of the project alongside the package.json that tells NPM to save the exact version number.

	# Save exact versions of NPM packages instead of allowing automatic updates.
	save-exact = true

### NVM

#### `.nvmrc`

[NVM](https://github.com/creationix/nvm) is a useful utility for managing versions of Node on a single machine. Some projects may require a newer version of Node than others and NVM makes it easy to switch between those versions. An `.nvmrc` file will force NVM to default to a specific, predetermined version of Node rather than typing nvm use <version number> every time.

	# Set the desired Node version below.
	5.7.0

## Comments

Be expressive with your code. Explain code as needed, but do your best to explain your code in functional and expressive ways without comments before falling back to a comment.

## General Formatting

### Indentation

Be consistent with tabs or spaces throughout a project. Do not mix tabs and spaces.

### Whitespace

Remove all trailing whitespace from lines of code. Introducing them can have unexpected results when diffing.

Optionally, if using Git, adjust your projects `.gitattributes` file to [accommodate expected whitespace](https://git-scm.com/book/tr/v2/Customizing-Git-Git-Configuration#_formatting_and_whitespace).

### Line Endings

When working on a project where team members are using Git for version control and both Windows and Mac for development, there may be [unexpected results](https://help.github.com/articles/dealing-with-line-endings/) after working on similar files. Discuss line endings with your team and [adjust the projects `.gitattributes` file](https://git-scm.com/book/tr/v2/Customizing-Git-Git-Configuration#_formatting_and_whitespace) accordingly.
