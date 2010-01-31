announcements
=============

_for announcements version 0.1.0_

Code for announcements is online at [GitHub](http://github.com): [http://github.com/pinax/django-announcements/tree/0.1.0](http://github.com/pinax/django-announcements/tree/0.1.0)

[Online usage documentation](http://github.com/pinax/django-announcements/blob/0.1.0/docs/usage.txt)

Data Model
----------

* Dependencies: 
	* django.contrib.auth
	
* Announcement

	* title (char 50)
	* content (text)
	* creator (foreign-key -> django.contrib.auth.models.User)
	* creation_date (datetime)
	* site_wide (boolean)
	* members_only (boolean)
	
	* Methods (AnnouncementManager) - Announcement.objects...
	
		* `current(self, exclude=[], site_wide=False, for_members=False)`
		
		Fetches and returns a queryset with the current announcements. This
        method takes the following parameters:
        
        ``exclude``
            A list of IDs that should be excluded from the queryset.
        
        ``site_wide``
            A boolean flag to filter to just site wide announcements.
        
        ``for_members``
            A boolean flag to allow member only announcements to be returned
            in addition to any others.
	
* Methods (notification.models...)

	* `current_announcements_for_request(request, **kwargs)`
	
		A helper function to get the current announcements based on some data from
	    the HttpRequest.

	    If request.user is authenticated then allow the member only announcements
	    to be returned.

	    Exclude announcements that have already been viewed by the user based on
	    the ``excluded_announcements`` session variable.
	
URL Design
----------

* pinax

	``(r'^announcements/', include('announcements.urls'))``

		`url(r"^(?P<object_id>\d+)/$", list_detail.object_detail,
		    announcement_detail_info, name="announcement_detail"),
		url(r"^(?P<object_id>\d+)/hide/$", announcement_hide,
		    name="announcement_hide"),
		url(r"^$", announcement_list, name="announcement_home"),`

Views & Templates
-----------------

* `announcement_list(request)`

	A basic view that wraps ``django.views.list_detail.object_list`` and
    uses ``current_announcements_for_request`` to get the current
    announcements.

* `announcement_hide(request, object_id)`
	
	Mark this announcement hidden in the session for the user.
	
TemplateTags
------------

_None_

Filters
-------

_None_

View Decorators
---------------

_None_

Forms
-----

_None_

ContextProcessor
----------------

* site\_wide\_announcements

	Adds the site-wide announcements to the global context of templates.
	
Constants
---------

* VERSION
