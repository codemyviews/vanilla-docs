=======
Logging
=======

We're using ``monolog/monolog`` to handle the logging.

----------------
Path to logfile?
----------------
The path to log folder is configured in ``/config/log.php``. The default value is ``{wordpress}/wp-contents/uploads/log``.

---------------------
Log a line by myself?
---------------------
To add a line to the logfile, you can call ``log_info($message)`` or ``log_error($message)`` helper functions

--------------
Several files?
--------------
The following example will log a 'line' to a file 'custom-file'::

   app()->log('custom-file')->info('line');

--------
Extended
--------
``app()->log('my-channel')`` returns a ``Monolog\Logger`` object with the 'channel' set to 'my-channel' and a single ``Monolog\Handler\StreamHandler`` configured to dump everything to the file ``/my-channel.log``

Logger Objects are stored based on the 'channel', so that several calls to the ``app()->log('channel')`` will return **the same** object. Please note this if adding additional handlers.