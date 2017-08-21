===============
Getting started
===============

------------
Why Vanilla?
------------

Because!

-------------------
Server Requirements
-------------------
Since Vanilla is a theme framework for WordPress it's server requirements are almost the same as for the WordPress itself:

* PHP >= 5.6
* MySQL >= 5.0 or any version of MariaDB

------------
Installation
------------

.. warning:: Text on this page is very close to the content of `Laravel installation docs <https://laravel.com/docs/5.4/installation>`_

Vanilla utilizes `Composer <https://getcomposer.org/>`_ to manage its dependencies. Make sure you have Composer installed on your machine.

First, download the Vanilla installer using Composer::

   composer global require "codemyviews/vanilla-installer"

Make sure to place the ``$HOME/.composer/vendor/bin directory`` (or the equivalent directory for your OS) in your $PATH so the vanilla executable can be located by your system.

Once installed, the ``vanilla new`` command will create a fresh wordpress installation with vanilla theme in the directory you specify. For instance, ``vanilla new blog`` will create a directory named blog containing a fresh Wordpress installation with the Vanilla theme installed and ready to work::

   vanilla new blog

-------------
Configuration
-------------

**Public Directory**
After installing Vanilla, you should configure your web server's document / web root to be the ``wordpress`` directory. Since the Vanilla is just a theme, we shall give the control to the wordpress installation.

**Using Laravel Valet**
If you're using Laravel Valet, note that you should link the site from ``wordpress`` folder, not from the project root.

**Configuration Files**
All of the configuration files for the Vanilla theme the config directory in the theme folder. Each option is documented, so feel free to look through the files and get familiar with the options available to you.
