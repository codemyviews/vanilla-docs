Post Type
=========

===================
What's a post type?
===================

    WordPress can hold and display many different types of content. A single item of such a content is generally called a post, although post is also a specific post type. Internally, all the post types are stored in the same place, in the wp_posts database table, but are differentiated by a column called post_type.

    -- `Wordpress Codex <https://codex.wordpress.org/Post_Types>`_

Post type is one of the fundamental entities in WordPress. Vanilla offers a PostType class to manage a different post type features.
Normally Vanilla PostType class feels a lot like a Model class in Laravel application.

============================
How do I create a post type?
============================

WordPress provide several post types out of the box, but often you would want to add a custom post type.
Examples might be a testimonial, or a portfolio item.

Command ``wp make:posttype Testimonial`` will add a new Testimonial post type.
It will create a new class in ``App\PostTypes`` folder and fill this class with default settings for you to modify.

===============================
How do I configure a post type?
===============================

---------------------
Single page templates
---------------------

Most of the post types you create would need a single page to view a particular post. You can provide a list of available templates for each post type to be used for the single post page.

By default this list look like this::

    protected $templates = [
        'Default' => 'default',
    ];

This declaration, tells Vanilla, that the default template to be used for the post type is ``default.blade.php``.
For our Testimonial post type, let's add a `With Avatar` and `Text only` templates. Also, lets change the default template.::

    protected $templates = [
        'Default' => 'testimonials/text-only',
        'Text Only' => 'testimonials/text-only',
        'With Avatar' => 'testimonials/with-avatar',
    ];

Now, the default template is  ``testimonials/text-only.blade.php``. All testimonial posts will also have a Template selector in the admin dashboard. With options `Default template`, `Text Only` and `With Avatar`

If Vanilla can't find a `Default` template for a post type, it will consider ``default.blade.php`` as a default template.

------------
Archive page
------------

Every post type can have an archive page that shows all existing posts of a given post type. You can manage the existence of such page by changing the value of ``$hasArchive`` variable in the PostType class. By default, all post types have an archive page.

The path to the archive page is configured with ``slug`` key in ``$names`` array. If it isn't provided, the ``$name`` is used instead.

The template for the archive page is configured via ``$archiveTemplate`` property in PostType class.

Let's enable the archive page for a Testimonial post type, and make it available in ``http://example.com/all-testimonials``. Use a ``testimonials/index.blade.php`` as a template for the archive page::

    protected $hasArchive = true;
    protected $archiveTemplate = 'testimonials/index';
    protected $names = [
        'slug' => 'all-testimonials'
    ];

> IMPORTANT: changes in slug and hasArchive properties affect WP rewrite rules and require calling ``wp flush-rewrites`` to be applied.

-------------
Custom fields
-------------

All post types has title and content fields. Yet, you would often want to add additional fields to the post type. It might be an address for a House post type, or a logo for Company post type.
Vanilla provides you a neat tool to manage custom fields. Under the hood Vanilla uses ACF (or ACF Pro) plugin

All PostType classes has a ``$fields`` property. This is how you add a custom `subtitle` text field to a post type::

    protected $fields = [
        'subtitle' => [
            'label' => 'Additional Heading',
            'type' => 'text'
        ]
    ];

You normally would want to provide `at least` ``type`` and ``label`` fields. But there are definitely more options for you to configure. Please address the `ACF documentation <https://www.advancedcustomfields.com/resources/>`_ for full list of available field types and configuration options.

If you want to use ACF Pro instead of ACF, you should manually install the plugin and update the ``custom_fields_driver`` property in ``/config/app.php`` to ``\Vanilla\Fields\Drivers\AcfPro::class``

--------------
Digging deeper
--------------

Under the hood Vanilla uses `Extended CPTs plugin <http://johnbillion.com/extended-cpts/>`_ to manage the post types. The plugin provides very wide range of available configuration options. Vanilla allows you to manage those directly via the `args()` method. To put it simple, array returned from `args()` method is merged into the arguments array passed to the ``register_custom_post_type()`` function.

This is how you add a new column to a posts table in the admin dashboard::

    protected function args() {
        return [
            'admin_cols' => [
                'published' => [
                    'title' => 'Published',
                    'meta_key' => 'published_date',
                    'date_format' => 'd/m/Y'
                ]
            ]
        ];
    }

