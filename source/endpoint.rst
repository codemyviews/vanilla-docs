Endpoint
========

===================
What's an endpoint?
===================

A lot of times you would need a custom endpoint in your site. For handling a contact form or creating an ajax driven application.
Vanilla allows you to create any number of custom endpoints to handle your requests.

============================
How do I create an endpoint?
============================
Command ``wp make:endpoint ContactForm`` will add a new ContactForm endpoint.
It will create a new class in ``App\Endpoints`` folder and fill this class with default settings for you to modify.

=========================
How do I use an Endpoint?
=========================
Each endpoint has a ``$name`` property and a ``handle()`` method.

All requests to the ``/endpoints/contact-form`` will trigger the ``handle()`` method on the endpoint with the ``$name`` set to the 'contact-form'.

``Endpoint::$name`` must be unique!

===============================
How do I configure an Endpoint?
===============================
--------------
Authentication
--------------
If you want to limit the access to the endpoint to only authenticated users, you can do so via ``$authOnly`` parameter.
When set to ``true``, the endpoint will only be executed for authenticated users. Others will get HTTP 401 error.

-------------
Authorization
-------------
Beside the authentication, you might want to add additional layers of authorization. You can do so by updating the ``authorized()`` method like this::

   protected function authorized() {
      return get_current_user_id() === 1;
   }

In this case the endpoint will only work for a user with id 1. All others will get HTTP 401 error.
