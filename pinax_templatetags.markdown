pinax.templatetags
==================

_for Pinax version 0.7.1_

Data Model
----------

_None_

URL Design
----------

_None_

Views & Templates
-----------------

_None_

TemplateTags
------------

* ifsetting
	* A node set assocaited with %else% and %endifsetting% that allows a control flow in the template based on the variable provided. The variable checks against the project's settings (settings.py) and will render (or not) the encapsulated content on a boolean check against the defined setting.
	* Example:
	
		`{% ifsetting ACCOUNT_OPEN_SIGNUP %} 
			content...
		{% else %}
			alternate content...
		{% endifsetting %}`

* fk_field
	* renders the `<a href...>` reference to the element using it's get_absolute_url() method
	* Example:
	
		`Object {% fk_field object_item %} has ...`

* mail_field
	* renders the `<a href="mailto:..."...>` reference to the element's value
	* Example:

		`Contact {{ user.first_name }} at {% mail_field user.email %} ...`

* order
	* reorders a list of objects by the provided attribute
	* Example:
	
		`{% order tasks by state %}`

* svn_app_version
	* returns the version of the pinax or django application using django.utils.version.get_svn_revision()
	* Example:
	
		`foo.app {% svn_app_version "foo.app" %}
	    project {% svn_app_version %}`

* silk
	* returns the image from the silk icons based on the name provided
	* Example:
	
		`{% silk "arrow_in" %}`
		
* var
	* allows you to set a variable using expressions within the template
	* Example:
	
		`{% var foo = expression %}
	    {% var foo = Model.foo_set.count %}
	    {% var foo = foo|restructuredtext %}
	    {{ foo }} {{ foo|escape }}`

Filters
-------

* in_list
	* tests if a value is in arg - assuming arg is a list. Based on [http://www.djangosnippets.org/snippets/379/](http://www.djangosnippets.org/snippets/379/)
	* Example:
	
		`The item is 
		{% if item|in_list:list %} 
		    in list 
		{% else %} 
		    not in list
		{% endif %}`

* shorttimesince
	* Formats a date as the time since that date (i.e. "4 days, 6 hours").
	* Example:
	
		`It was {{ x.last_saved|shorttimesince }} since it was edited.`

View Decorators
---------------

_None_

Forms
-----

_None_

Constants
---------

_None_
