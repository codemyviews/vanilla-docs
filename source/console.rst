=======
Console
=======
------
WP-CLI
------
.. warning:: TODO: add a wp-cli as a composer dependency

We're using `WP-CLI <http://wp-cli.org/>`_ to handle a console commands. This means, all the commands that are shipped with the wp-cli package are available in Vanilla installations.

----------------
Vanilla commands
----------------
Vanilla provides numerous neat commands out of the box:

* ``wp flush-rewrites`` flushes the cached rewrite rules.
* ``wp make:posttype {name}`` creates new post type
* ``wp make:taxonomy {name}`` creates new taxonomy
* ``wp make:endpoint {name}`` creates new endpoint
* ``wp make:command {name}`` creates new command (see below)

------------------
Adding new command
------------------
``wp make:command hello`` command will create a command class in App/Commands folder of your Vanilla theme.

``$name`` attribute in the command class defines the way you would call the command from the console. In our example, $name would be set to hello and to call the command you will have to type ``wp hello`` in the console.

``$description`` attribute defines the short description displayed by the ``wp help`` command

``handle($args, $named)`` method is called when the command is executed. The method accepts two parameters:
``$args`` is an array of unnamed command parameters provided by the user. For example, in ``wp hello bob mary`` call, $args will contain two strings: ``['bob', 'mary']``
``$named`` is an array of named command parameters provided by the user. For example, in ``wp hello --name=bob --from=mary`` call, $named will look like this: ``['name' => 'bob', 'from' => 'mary']``