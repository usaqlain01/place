[![Build Status](https://travis-ci.org/drupal-composer/drupal-project.svg?branch=8.x)](https://travis-ci.org/drupal-composer/drupal-project)
# Usman Saqlein's Drupal Kick Start Application

Following Project implements Drupal CRM for quick, Proof of Concept Application & Code Samples.

## Installation

1. clone the project in a directory:
```
git clone git@github.com:usaqlein/place.git
```
1. Run ``` composer install ``` on the Root directory
1. Root directory contains **place_dev.sql** file, Create a **MySQL database** and import it to the database.
1. Inside the Root is a folder **Web** which is **Drupal Root** and contains **index.php** file, This will trigger Application Install Process (first-time).
1. Application will ask for Database credentials and setup the connection, please point it to where database file was imported in step 2.
1. Composer should set the correct permissions on the files, however if you run into an issue, plz chmod a+w the root/web/sites/default/* dir.
1. Please select **standard installation** and once finished follow **Configuration >> Development** (top admin bar) and clear the cache.
1. Additional documentation on Installation process can be found here: [drupal 8 Installation](https://www.drupal.org/docs/user_guide/en/install-run.html).
1. I will be pushing this code to the Live Server as well. Please visit
```
http://45.55.61.100
```
To see a live demo for this repository.


## Developing on Kick Starter Application

This project will attempt to keep all of your Drupal Core files up-to-date; the 
project [drupal-composer/drupal-scaffold](https://github.com/drupal-composer/drupal-scaffold) 
is used to ensure that your scaffold files are updated every time drupal/core is 
updated. If you customize any of the "scaffolding" files (commonly .htaccess), 
you may need to merge conflicts if any of your modified files are updated in a 
new release of Drupal core.

Follow the steps below to update your core files.

1. Run `composer update drupal/core --with-dependencies` to update Drupal Core and its dependencies.
1. Run `git diff` to determine if any of the scaffolding files have changed. 
   Review the files for any changes and restore any customizations to 
  `.htaccess` or `robots.txt`.
1. Commit everything all together in a single commit, so `web` will remain in
   sync with the `core` when checking out branches or running `git bisect`.
1. In the event that there are non-trivial conflicts in step 2, you may wish 
   to perform these steps on a branch, and use `git merge` to combine the 
   updated core files with your customized files. This facilitates the use 
   of a [three-way merge tool such as kdiff3](http://www.gitshah.com/2010/12/how-to-setup-kdiff-as-diff-tool-for-git.html). This setup is not necessary if your changes are simple; 
   keeping all of your modifications at the beginning or end of the file is a 
   good strategy to keep merges easy.

## Generate composer.json from existing project

With using [the "Composer Generate" drush extension](https://www.drupal.org/project/composer_generate)
you can now generate a basic `composer.json` file from an existing project. Note
that the generated `composer.json` might differ from this project's file.


## FAQ

### Should I commit the contrib modules I download?

Composer recommends **no**. They provide [argumentation against but also 
workrounds if a project decides to do it anyway](https://getcomposer.org/doc/faqs/should-i-commit-the-dependencies-in-my-vendor-directory.md).

### Should I commit the scaffolding files?

The [drupal-scaffold](https://github.com/drupal-composer/drupal-scaffold) plugin can download the scaffold files (like
index.php, update.php, …) to the web/ directory of your project. If you have not customized those files you could choose
to not check them into your version control system (e.g. git). If that is the case for your project it might be
convenient to automatically run the drupal-scaffold plugin after every install or update of your project. You can
achieve that by registering `@drupal-scaffold` as post-install and post-update command in your composer.json:

```json
"scripts": {
    "drupal-scaffold": "DrupalComposer\\DrupalScaffold\\Plugin::scaffold",
    "post-install-cmd": [
        "@drupal-scaffold",
        "..."
    ],
    "post-update-cmd": [
        "@drupal-scaffold",
        "..."
    ]
},
```
### How can I apply patches to downloaded modules?

If you need to apply patches (depending on the project being modified, a pull 
request is often a better solution), you can do so with the 
[composer-patches](https://github.com/cweagans/composer-patches) plugin.

To add a patch to drupal module foobar insert the patches section in the extra 
section of composer.json:
```json
"extra": {
    "patches": {
        "drupal/foobar": {
            "Patch description": "URL or local path to patch"
        }
    }
}
```
### How do I switch from packagist.drupal-composer.org to packages.drupal.org?

Follow the instructions in the [documentation on drupal.org](https://www.drupal.org/docs/develop/using-composer/using-packagesdrupalorg).
