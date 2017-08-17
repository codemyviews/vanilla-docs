Querying
========

WP_Query is confusing. That's why ended up putting together an additional layer around it so that querying posts will become enjoying.

===========
Basic usage
===========

The following example will show the titles of all posts with the ``Chapter`` post type::

   <ul>
   @foreach(App\PostTypes\Chapter::all() as $chapter)
      <li>{{ $chapter->title() }}</li>
   @endforeach
   </ul>

You can also create a query builder without using a post type, which might be usable when you don't want the post type restriction.
This is how it's done::

   @foreach(query()->get() as $post)
      <h1>{{ $post->title() }} </h1>
   @endforeach

Please note, that if post types are not specified in the query builder - all post types from app/PostTypes will be used.

The ``$post`` variable in both examples will contain an **object** of a relevant PostType class. At the same time, the_post(), the_ID() and all other WP functions that work inside WP query, will also work and will be pointed to the correct post.
You can access any property of ``the_post()`` on the ``$post``::

   @foreach(query()->type('post')->get() as $post)
      <h1>{{ $post->guid }} === {{ get_post()->guid }}</h1>
   @endforeach

This allows you to add custom logic to the PostType class and use it in the templates.

=======
Options
=======

------
Author
------

You can specify the login of the Author::

   query()->author('john')->get()

Or use Id instead::

   query()->author(2)->get()

Or several::

   query()->author([2, 15, 'bob'])->get()

You can also use a `authorNot` method. It's interface is exactly the same, but will exclude posts from a given author instead.::

   query()->authorNot('unwanted')->get()

.. warning:: Note, that if the method is called several times, only the latest call is used.

-------
Post ID
-------
It is possible to specify a particular post id to fetch::

   query()->post(2)

List of ids is also available::

   query()->post([1, 13, 43])

If you want to exclude ids, you can use ``postNot`` method::

   query()->postNot(13)

Multiple exclusion is also available::

   query()->postNot(9, 11)

.. warning:: Note, that if the method is called several times, only the latest call is used.

---------
Post Type
---------
If you want to manually specify a list of queried post types, you can use a ``type()`` method::

   query()->type('post')

As always, array as an argument is also available::

   query()->type(['post', 'page'])

If you start a query using a PostType class, this post type is automatically added as a queried post type.::

   App\PostTypes\Post::all()

Acts exactly the same as::

   query()->type('post')->get()

.. warning:: multiple calls to the ``type()`` method are combined!  ``App\PostTypes\Post::type('page')->type('company')`` will query 'post', 'page' and 'company' post types


------
Parent
------
To specify a required parent post use::

   query()->parent(23)

You can also provide a list of parent ids::

   query()->parentIn([11, 23])

To query only the posts with no parent (first level posts)::

   query()->noParent()

----
Slug
----
You can also query a post using it's name::

   query()->slug('hello-world')

------
Status
------

Query by status::

   query()->status('published')

------
Search
------

You can use a built-in WP search logic with the ``search()`` method::

   query()->search('query')

-----
Order
-----

Simple::

   query()->orderBy('name')
   query()->orderBy('name', 'ASC')
   query()->orderBy('id name', 'DESC')

Complex::

   query()->orderBy(['name' => 'ASC', 'id' => 'DESC'])

Special cases::

   query()->orderBy('rand')
   query()->orderBy('none')

------------
Sticky posts
------------
By default WP will put sticky posts on top of the query results no matter the requested ordering. To override this behaviour and ignore post stickiness, there is a ``ignoreStickyPosts()`` method.::

   query()->ignoreStickyPosts()

----------------
Offset and Limit
----------------
If you need to use limit and offset the query results without using the pagination, you could use the ``offset()`` and ``limit()`` methods.::

   query()->offset(3)->limit(5)

==========
Pagination
==========

``query()->paginate($perPage)`` method returns a ``Vanilla\Paginator`` object.

Basic usage Example::

   <?php $paginator = App\PostTypes\Post::paginate(3); ?>

   @foreach($paginator->items() as $post)
      <h4>{{ $post->title() }} from {{ $post->post_date }}</h4>
   @endforeach

   @if($paginator->hasPreviousPage())
      <a href="{{ $paginator->previousPageUrl() }}">Previous</a>
   @endif

   Page: {{ $paginator->currentPage() }} of {{ $paginator->pages() }}

   @if($paginator->hasNextPage())
      <a href="{{ $paginator->nextPageUrl() }}">Next</a>
   @endif

To create a link to a custom page number, you could use the following example::

   <a href="{{ $paginator->linkToPage(5) }}"> Go to fifth page </a>
   <a href="{{ $paginator->linkToPage(21) }}"> Go to page 21</a>

------
Manual
------
There are methods for manual pagination control::

   query()->perPage(3)->page(2)->paginator()

Please note that the following will also work, but will return the query results instead of Paginator object::

   query()->perPage(20)->page(3)->get()
