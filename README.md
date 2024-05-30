**Quickly spin up a new Filament powered application.**

Filament Installer is a command-line tool that replaces the Laravel installer and wraps up the most common tasks you might take when creating a Filament app: opening it in your editor and your browser, initialize a git repository, tweak your `.env` and `.env.example`, and more.

# Requirements

- PHP 8.2+

# Installation

```bash
composer global require shanerbaner82/filament-installer
```

# Upgrading

```bash
composer global update shanerbaner82/filament-installer
```

# Usage

Make sure `~/.composer/vendor/bin` is in your terminal's path.

```bash
cd ~/<code-directory>
filament new my-cool-filament-app
```

# What exactly does it do?

- `filament new $PROJECTNAME`
- Initialize a git repo, add all the files, and, after some changes below, make a commit with the text "Initial commit."
- Replace the `.env` (and `.env.example`) database credentials with the default macOS MySQL credentials: database of `$PROJECTNAME`, user `root`, and empty password
- Replace the `.env` (and `.env.example`) `APP_URL` with `$PROJECTNAME.$YOURVALETTLD`
- Generate an app key
- Set up dark mode (if opted in)
- Scaffold custom theme assets (if opted in)
- Install and setup [Filament Breezy](https://filamentphp.com/plugins/breezy), [Filament Shield](https://filamentphp.com/plugins/shield), or [Filament Sentry](https://github.com/awcodes/filament-sentry) (if opted in)
- Open the project in your favorite editor
- Open `$PROJECTNAME.$YOURVALETTLD` in your browser

> Note: If your `$PROJECTNAME` has dashes (`-`) in it, they will be replaced with underscores (`_`) in the database name.

There are also a few optional behaviors based on the parameters you pass (or define in your config file), including creating a database, migrating, running Valet Link and/or Secure, and running a custom bash script of your definition after the fact.
