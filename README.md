dreamhost/php-compat-command
==================================

Scan WordPress, plugins and themes for PHP version compatibility.

Forked from [php-compat-command by Daniel Bachhuber](https://github.com/danielbachhuber/php-compat-command]

Quick links: [Using](#using) | [Installing](#installing) | [Contributing](#contributing) | [Support](#support)

## Using

~~~
wp php-compat [--path=<path>] [--php_version=<version>] [--fields=<fields>] [--format=<format>]
~~~

Uses the [PHPCompatibility PHPCS sniffs](https://github.com/wimg/PHPCompatibility)
and interprets the WordPress-specific results. Defaults to '7.0-' for scanning
PHP 7.0 and above.

If a theme or plugin is compatible, it results with `compat=success`. If there's
an incompatibility, it results with `compat=failure`.

Speed up the scanning process by using [php-compat-cache](https://github.com/danielbachhuber/php-compat-cache), a collection of
pre-scanned WordPress.org plugins and themes. If a theme or plugin is known to
be compatible with
an update, it results `compat=with-update`.

**OPTIONS**

	[--path=<path>]
		Path to the WordPress install. Defaults to current directory.

	[--php_version=<version>]
		Scan for support of a particular PHP version. Use '-' to indicate equal
		or greater than (e.g. 7.0- for PHP 7.0 and above).
		---
		default: 7.0-
		---

	[--fields=<fields>]
		Limit output to specific fields.

	[--format=<format>]
		Render output in a particular format.
		---
		default: table
		options:
		  - table
		  - csv
		  - json
		  - yaml
		---

**EXAMPLES**

    # Check compatibility of a WordPress install in the 'example.com' path
    $ wp php-compat --path=example.com
    +-----------------------+--------+---------+---------+-------+-------+
    | name                  | type   | compat  | version | time  | files |
    +-----------------------+--------+---------+---------+-------+-------+
    | wordpress             | core   | success | 4.7.6   |       |       |
    | akismet               | plugin | success | 3.2     | 1.39s | 13    |
    | debug-bar             | plugin | success | 0.8.4   | 0.29s | 10    |
    | oembed-gist           | plugin | success | 4.7.1   | 0.08s | 1     |
    | danielbachhuber-theme | theme  | success | 0.0.0   | 0.81s | 30    |
    | twentyfifteen         | theme  | success | 1.7     | 0.42s | 22    |
    | twentyseventeen       | theme  | success | 1.1     | 0.63s | 35    |
    | twentysixteen         | theme  | success | 1.3     | 0.5s  | 23    |
    +-----------------------+--------+---------+---------+-------+-------+

    # Use php-compat-cache to speed up scanning process
    $ git clone https://github.com/danielbachhuber/php-compat-cache.git ~/php-compat-cache
    $ WP_CLI_PHP_COMPAT_CACHE=~/php-compat-cache wp php-compat --path=example.com
    +-----------------------+--------+---------+---------+--------+-------+
    | name                  | type   | compat  | version | time   | files |
    +-----------------------+--------+---------+---------+--------+-------+
    | wordpress             | core   | success | 4.7.6   | cached |       |
    | akismet               | plugin | success | 3.2     | cached | 13    |
    | debug-bar             | plugin | success | 0.8.4   | 0.14s  | 10    |
    | oembed-gist           | plugin | success | 4.7.1   | 0.07s  | 1     |
    | danielbachhuber-theme | theme  | success | 0.0.0   | 0.36s  | 30    |
    | twentyfifteen         | theme  | success | 1.7     | cached | 22    |
    | twentyseventeen       | theme  | success | 1.1     | cached | 35    |
    | twentysixteen         | theme  | success | 1.3     | cached | 23    |
    +-----------------------+--------+---------+---------+--------+-------+

    # Plugin is known to be compatible with an update
    $ WP_CLI_PHP_COMPAT_CACHE=~/php-compat-cache wp php-compat
    +-----------------+--------+--------------+---------+--------+-------+
    | name            | type   | compat       | version | time   | files |
    +-----------------+--------+--------------+---------+--------+-------+
    | wordpress       | core   | success      | 4.9.8   | cached |       |
    | akismet         | plugin | success      | 4.0.8   | cached | 13    |
    | woocommerce     | plugin | with-update  | 3.2.6   | cached |       |
    | twentyfifteen   | theme  | success      | 2.0     | 0.25s  | 22    |
    | twentyseventeen | theme  | success      | 1.7     | 0.3s   | 35    |
    | twentysixteen   | theme  | success      | 1.5     | 0.28s  | 23    |
    +-----------------+--------+--------------+---------+--------+-------+

## Installing

Installing this package requires WP-CLI v2 or greater. Update to the latest stable release with `wp cli update`.

Once you've done so, you can install this package with:

    wp package install git@github.com:dreamhost/php-compat-command.git

### Reporting a bug

Think you’ve found a bug? We’d love for you to help us get it fixed.

Before you create a new issue, you should [search existing issues](https://github.com/dreamhost/php-compat-command/issues?q=label%3Abug%20) to see if there’s an existing resolution to it, or if it’s already been fixed in a newer version.

Once you’ve done a bit of searching and discovered there isn’t an open or fixed issue for your bug, please [create a new issue](https://github.com/dreamhost/php-compat-command/issues/new). Include as much detail as you can, and clear steps to reproduce if possible.

### Creating a pull request

Want to contribute a new feature? Please first [open a new issue](https://github.com/dreamhost/php-compat-command/issues/new) to discuss if the feature is a good fit for the project.

## Support

Github issues aren't for general support questions, but there are other venues you can try: https://wp-cli.org/#support


*This README.md is generated dynamically from the project's codebase using `wp scaffold package-readme` ([doc](https://github.com/wp-cli/scaffold-package-command#wp-scaffold-package-readme)). To suggest changes, please submit a pull request against the corresponding part of the codebase.*
