=============
Configuration
=============

Configuration files are available at /config folder of the Vanilla theme.

The following example will try to access the "name" value from /config/app.php. If such value exists, it will be returned. Otherwise, string 'Vanilla' will be returned, otherwise, the string 'Vanilla' will be returned.::

   app()->config('name', 'Vanilla')

This is also a valid call. If no default value is provided, null will be returned as a default value.::

   app()->config('name')

If you need to access configuration value from file other than `config/app.php`, you should prefix the configuration key with the filename and a dot.
The following example will attempt to fetch the `path` value from `config/log.php`.::

   app()->config('log.path')

You can even do stuff like::

   app()->config('folder.folder.file.key')

.. warning:: Test the ``app()->config('folder.folder.file.key')`` it might not actually work!
