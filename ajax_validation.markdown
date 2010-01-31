ajax_validation
===============

_for ajax\_validation version 0.1.3__

Code for ajax\_validation is online at [GitHub](http://github.com): [http://github.com/alex/django-ajax-validation/tree/0.1.3](http://github.com/alex/django-ajax-validation/tree/0.1.3)

[Online usage documentation](http://github.com/alex/django-ajax-validation/blob/0.1.3/docs/usage.txt)

_Note:_ Ajax validation isn't used on it's own as an application, but it referenced in other Django and Pinax applications which use this as a separate library. The mechanism has a dependency on jQuery to function.

Data Model
----------

_None_
	
URL Design
----------

	`(r'^SOME/URL/$', 'ajax_validation.views.validate', {'form_class': ContactForm}, 'contact_form_validate')`
	
Views & Templates
-----------------

* `validate(request, *args, **kwargs)`
	
TemplateTags
------------

* include_validation
	* renders in jQuery for ajax validation

		`{% include_validation %}`

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
