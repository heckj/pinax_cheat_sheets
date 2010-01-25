django.contrib.sites
====================

_for Django version 1.1_

Data Model
----------

Dependency: _None_

* Site

	* domain (char 100)
	* name (char 50)

	* Methods (SiteManager) - Site.objects...
	
		* `get_current(self)`
		
	        Returns the current ``Site`` based on the SITE_ID in the
	        project's settings. The ``Site`` object is cached the first
	        time it's retrieved from the database.
	
		* `clear_cache(self)`
		
			Clears the ``Site`` object cache.
	
	* Methods - User...
	
		* save(self, *args, **kwargs) - saves a site object
		* delete(self) - deletes the site

* RequestSite

	A class that shares the primary interface of Site (i.e., it has
    ``domain`` and ``name`` attributes) but gets its data from a Django
    HttpRequest object rather than from a database.

    The save() and delete() methods raise NotImplementedError.
    
	* user (foreignkey -> User)
	* message (text)

URL Design
----------

_None_

Views & Templates
-----------------

_None_

View Decorators
---------------

_None_

Forms
-----

_None_

Constants
---------

* SITE_ID (from settings.py)
