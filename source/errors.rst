==============
Error Handling
==============

404 page template is configured by ``not_found_template`` in  ``config/app.php``

Other error pages are shown based on the WP_DEBUG value. If WP_DEBUG is set to true, Vanilla will render a neat error page using ``filp/whoops`` library.
If WP_DEBUG is set to a false, Vanilla will render a simple error page. You can provide a custom template to be used in this case using ``custom_error_template`` property in ``/config/app.php``