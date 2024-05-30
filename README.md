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
composer global update awcodes/filament-installer
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

# Customizing Filament Installer

While the default actions Filament Installer provides are great, most users will want to customize at least a few of the steps. Thankfully, Filament Installer is built to be customized!

There are three ways to customize your usage of Filament Installer: command-line arguments, a config file, and an "after" file.

Most users will want to set their preferred configuration options once and then never think about it again. That's best solved by creating a config file.

But if you find yourself needing to change the way you interact with Filament Installer on a project-by-project basis, you may also want to use the command-line parameters to customize Filament Installer when you're using it.

## Creating a config file

You can create a config file at `~/.filament/config` rather than pass the same arguments each time you create a new project.

The following command creates the file, if it doesn't exist, and edits it:

```bash
filament edit-config
```

The config file contains the configuration parameters you can customize, and will be read on every usage of Filament Installer.

## Creating an "after" file

You can also create an after file at `~/.filament/after` to run additional commands after you create a new project.

The following command creates the file, if it doesn't exist, and edits it:

```bash
filament edit-after
```

The after file is interpreted as a bash script, so you can include any commands here, such as installing additional composer dependencies...

```bash
# Install additional composer dependencies as you would from the command line.
echo "Installing Composer Dependencies"
composer require awcodes/filament-quick-create spatie/laravel-ray
```

...or copying additional files to your new project.

```bash
# To copy standard files to new filament project place them in ~/.filament/includes directory.
echo "Copying Include Files"
cp -R ~/.filament/includes/ $PROJECTPATH
```

You also have access to variables from your config file such as `$PROJECTPATH` and `$CODEEDITOR`.

## Using command-line parameters

Any command-line parameters passed in will override Filament Installer's defaults and your config settings. See a [full list of the parameters you can pass in](#parameters).

# Filament Installer Commands

- `help` or `help-screen` show the help screen

<a id="config-files"></a>
- `edit-config` edits your config file (and creates one if it doesn't exist)

  ```bash
  filament edit-config
  ```

- `edit-after` edits your "after" file (and creates one if it doesn't exist)

  ```bash
  filament edit-after
  ```


<a id="parameters"></a>
# Configurable parameters

You can optionally pass one or more of these parameters every time you use Filament Installer. If you find yourself wanting to configure any of these settings every time you run Filament Installer, that's a perfect use for the [config files](#config-files).

- `-e` or `--editor` to define your editor command. Whatever is passed here will be run as `$EDITOR .` after creating the project.

  ```bash
  # runs "subl ." in the project directory after creating the project
  filament new my-cool-filament-app --editor=subl
  ```

- `-p` or `--path` to specify where to install the application.

  ```bash
  filament new my-cool-filament-app --path=~/Sites
  ```

- `-m` or `--message` to set the first Git commit message.

  ```bash
  filament new my-cool-filament-app --message="This filament runs fast!"
  ```

- `-f` or `--force` to force install even if the directory already exists

  ```bash
  # Creates a new Laravel application after deleting ~/Sites/my-cool-filament-app
  filament new my-cool-filament-app --force
  ```

- `-d` or `--dev` to choose the `develop` branch instead of `master`, getting the beta install.

  ```bash
  filament new my-cool-filament-app --dev
  ```

- `-b` or `--browser` to define which browser you want to open the project in.

  ```bash
  filament new my-cool-filament-app --browser="/Applications/Google Chrome Canary.app"
  ```

- `-l` or `--link` to create a Valet link to the project directory.

  ```bash
  filament new my-cool-filament-app --link
  ```

- `-s` or `--secure` to secure the Valet site using https.

  ```bash
  filament new my-cool-filament-app --secure
  ```

- `--create-db` to create a new MySQL database which has the same name as your project.
  This requires `mysql` command to be available on your system.

  ```bash
  filament new my-cool-filament-app --create-db
  ```

- `--migrate-db` to migrate your database.

  ```bash
  filament new my-cool-filament-app --migrate-db
  ```

- `--dbuser` to specify the database username.

  ```bash
  filament new my-cool-filament-app --dbuser=USER
  ```

- `--dbpassword` specify the database password.

  ```bash
  filament new my-cool-filament-app --dbpassword=SECRET
  ```

- `--dbhost` specify the database host.

  ```bash
  filament new my-cool-filament-app --dbhost=127.0.0.1
  ```

- `--dark` to use the Filament dark mode by default.

  ```bash
  filament new my-cool-filament-app --dark
  ```

- `--themed` to scaffold out the assets needed for a custom Filament theme.

  ```bash
  filament new my-cool-filament-app --themed
  ```

- `--mix` to revert Laravel to Laravel Mix instead of Vite

  ```bash
  filament new my-cool-filament-app --mix
  ```

- `--breezy` to install and setup Filament Breezy (authentication plugin).

  ```bash
  filament new my-cool-filament-app --breezy
  ```

- `--shield` to install and setup Filament Shield (authorization plugin).

  ```bash
  filament new my-cool-filament-app --shield
  ```

- `--sentry` to install and setup Filament Sentry (authentication, with Breezy, authorization, with Shield and Filament User Resources plugin).

  ```bash
  filament new my-cool-filament-app --sentry
  ```

- `--full` to use `--create-db`, `--migrate-db`, `--link`, and `-secure`.

  ```bash
  filament new my-cool-filament-app --full

**GitHub Repository Creation**

**Important:** To create new repositories Filament Installer requires one of the following tools to be installed:
- the official [GitHub command line tool](https://github.com/cli/cli#installation)
- the [hub command line tool](https://github.com/github/hub#installation)

Filament Installer will give you the option to continue without GitHub repository creation if neither tool is installed.

- `-g` or `--github` to  Initialize a new private GitHub repository and push your new project to it.

```bash
# Repository created at https://github.com/<your_github_username>/my-cool-filament-app
filament new my-cool-filament-app --github
```

- Use `--gh-public` with `--github` to make the new GitHub repository public.

```bash
filament new my-cool-filament-app --github --gh-public
```

- Use `--gh-description` with `--github` to initialize the new GitHub repository with a description.

```bash
filament Installer new my-cool-filament-app --github --gh-description='My cool Filament application'
```
- Use `--gh-homepage` with `--github` to initialize the new GitHub repository with a homepage url.

```bash
filament Installer new my-cool-filament-app --github --gh-homepage=https://example.com
```
- Use `--gh-org` with `--github` to initialize the new GitHub repository with a specified organization.

```bash
# Repository created at https://github.com/acme/my-cool-filament-app
filament new my-cool-filament-app --github --gh-org=acme
```