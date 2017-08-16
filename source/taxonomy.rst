Taxonomy
========

==================
What's a taxonomy?
==================

    Taxonomy is one of those words that most people never hear or use. Basically, a taxonomy is a way to group things together.

    -- `Wordpress Codex <https://codex.wordpress.org/Taxonomies>`_

Taxonomy is one of the fundamental entities in WordPress. Example taxonomies are ``category`` and ``tag``. You can also think of ``family`` or ``network`` as a taxonomy examples.
Vanilla offers a Taxonomy class to manage a different taxonomy features.

===========================
How do I create a taxonomy?
===========================
As was mentioned before, WordPress provide several taxonomies out of the box, but often you would want to add a custom taxonomy.
Examples might be a family, or a network.

Command ``wp make:taxonomy Family`` will add a new Family taxonomy.
It will create a new class in ``App\Taxonomies`` folder and fill this class with default settings for you to modify.

Note that you wont be able to use new taxonomy until you configure the post types for the taxonomy to be available for.

==============================
How do I configure a taxonomy?
==============================
------------
Archive page
------------

.. warning:: Add a ``$names`` and ``$archiveTemplate`` to the Taxonomy stub!

Every taxonomy has an archive page that shows all existing posts in a given taxonomy.

The path to the archive page is configured with ``slug`` key in ``$names`` array. If it isn't provided, the ``$name`` is used instead.

The template for the archive page is configured via ``$archiveTemplate`` property in Taxonomy class.

Let's configure the archive page for a Family taxonomies, and make it available in ``http://example.com/families/{family-name}``. Use a ``taxonomies/family.blade.php`` as a template for the archive page::

    protected $archiveTemplate = 'taxonomies/family';
    protected $names = [
        'slug' => 'families'
    ];

.. warning:: Changes in slug affect WP rewrite rules and require calling ``wp flush-rewrites`` to be applied.

----------
Post Types
----------

A taxonomy can be available for a numerous post types. The list of post types connected with the taxonomy is configured in the Taxonomy class via ``$postTypes`` parameter.

Lets add our ``Family`` taxonomy to a custom ``Person`` post type:::

   $postTypes = [
      App\PostTypes\Person::class
   ]

After that you will be able to select Family for a Person on a Person editing page. Neat.



