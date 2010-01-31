markdown template
=================

_for pagination version 1.0.5.1_

Code for pagination is online at [GitHub](http://github.com): [http://github.com/brosner/django-pagination](http://github.com/brosner/django-pagination) and at Google Code at  [http://code.google.com/p/django-pagination/](http://code.google.com/p/django-pagination/)

[Online usage documentation](http://github.com/brosner/django-pagination/blob/master/docs/usage.txt)

Data Model
----------

* Dependencies: _None_

URL Design
----------

_None_

Views & Templates
-----------------

* Embedded Default Templates
	* _from django pagination
		* pagination/pagination.html [http://github.com/brosner/django-pagination/blob/master/pagination/templates/pagination/pagination.html](http://github.com/brosner/django-pagination/blob/master/pagination/templates/pagination/pagination.html)
	
TemplateTags
------------

* autopaginate
	* Add this line at the top of your template to load the pagination tags:

	       `{% load pagination_tags %}`

	* Decide on a variable that you would like to paginate, and use the
	   autopaginate tag on that variable before iterating over it.  This could 
	   take one of two forms (using the canonical ``object_list`` as an example
	   variable):

	       `{% autopaginate object_list %}`

	   This assumes that you would like to have the default 20 results per page.
	   If you would like to specify your own amount of results per page, you can
	   specify that like so:

	       `{% autopaginate object_list 10 %}`

	   Note that this replaces ``object_list`` with the list for the current page, so
	   you can iterate over the ``object_list`` like you normally would.


* paginate
	* Now you want to display the current page and the available pages, so
	   somewhere after having used autopaginate, use the paginate inclusion tag:

	       `{% paginate %}`

	   This does not take any arguments, but does assume that you have already
	   called autopaginate, so make sure to do so first.

Filters
-------

_None_

View Decorators
---------------

_None_

Forms
-----

_None_

Constants
---------

* VERSION

* settings.PAGINATION\_DEFAULT\_PAGINATION (default 20)
* settings.PAGINATION\_DEFAULT\_WINDOW (default 4)
* settings.PAGINATION\_DEFAULT\_ORPHANS (default 0)
* settings.PAGINATION\_INVALID\_PAGE\_RAISES\_404 (default False)