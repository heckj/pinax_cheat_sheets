timezones
=========

_for timezones version 0.1.4_

Code for django-notification is online at [GitHub](http://github.com): [http://github.com/brosner/django-timezones/tree/0.1.X](http://github.com/brosner/django-timezones/tree/0.1.X)

[Online usage documentation](http://github.com/brosner/django-timezones/blob/0.1.X/docs/how_to_use.txt)

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

_None_

Filters
-------

* localtime
	* returns the local time for the timezone setting
	* Example:

		`{{ message.sent_at|localtime:account.timezone|date:_("DATETIME_FORMAT") }}`

View Decorators
---------------

_None_

Forms
-----

* TimeZoneField(forms.ChoiceField)

* LocalizedDateTimeField(forms.DateTimeField)

	Converts the datetime from the user timezone to settings.TIME_ZONE.
	
Constants
---------

* VERSION
