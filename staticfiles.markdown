staticfiles
===========

_for staticfiles version 0.1.2_

Code for django-notification is online at [GitHub](http://github.com): [http://github.com/jezdez/django-staticfiles/tree/0.1.2](http://github.com/jezdez/django-staticfiles/tree/0.1.2)

[Online usage documentation](http://github.com/jezdez/django-staticfiles/blob/0.1.2/README)

Data Model
----------

_None_
	
URL Design
----------

	(r'^static/(?P<path>.*)$', 'staticfiles.views.serve'),
	(r'^media/(?P<path>.*)$', 'django.views.static.serve', {
	    'document_root': settings.MEDIA_ROOT
	}),

Views & Templates
-----------------

* `serve(request, path, show_indexes=False)`

	Serve static files below a given point in the directory structure.

    To use, put a URL pattern such as::

        (r'^(?P<path>.*)$', 'staticfiles.views.serve')

    in your URLconf. You may also set ``show_indexes`` to ``True`` if you'd
    like to serve a basic index of the directory.  This index view will use
    the template hardcoded below, but if you'd like to override it, you
    can create a template called ``static/directory_index``.
	
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

Constants
---------

* VERSION

* settings.STATIC\_ROOT

	`STATIC_ROOT = ''`
	
	Pinax uses: `STATIC_ROOT = os.path.join(PROJECT_ROOT, 'site_media', 'static')`
	
* settings.STATIC\_URL

	`STATIC_URL = ''`
	
	Pinax uses: `STATIC_URL = '/site_media/static/'`

* settings.STATICFILES\_DIRS

	`STATICFILES\_DIRS = []`
	
	Pinax uses: `STATICFILES_DIRS = (
	    ('basic_project', os.path.join(PROJECT_ROOT, 'media')),
	    ('pinax', os.path.join(PINAX_ROOT, 'media', PINAX_THEME)),
	)`
	
* settings.STATICFILES\_MEDIA\_DIRNAMES

	`STATICFILES\_MEDIA\_DIRNAMES = ('media',)`

* settings.STATICFILES\_PREPEND\_LABEL\_APPS

	`STATICFILES\_PREPEND\_LABEL\_APPS = ('django.contrib.admin',)`
	
* settings.STATICFILES\_EXCLUDED\_APPS

	`STATICFILES\_EXCLUDED\_APPS = []`
