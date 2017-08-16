Querying
========

WP_Query is confusing. That's why ended up putting together an additional layer around it so that querying posts will become enjoying.

===========
Basic usage
===========

The following example will show the titles of all posts with the ``Chapter`` post type::

   <ul>
   @foreach(App\PostTypes\Chapter::all() as $chapter)
      <li>{{ $chapter->title }}</li>
   @endforeach
   </ul>

==========
Pagination
==========

``Vanilla\Query\Builder::paginate($perPage)`` method returns a ``Vanilla\Paginator`` object.

Basic Example::

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

