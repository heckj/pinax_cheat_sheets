django.contrib.humanize
=======================

_for Django version 1.1_

http://docs.djangoproject.com/en/1.1/ref/contrib/humanize/#ref-contrib-humanize

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

* ordinal
	* Converts an integer to its ordinal as a string. 1 is '1st', 2 is '2nd', 3 is '3rd', etc. Works for any integer.

* intcommon
	* Converts an integer to a string containing commas every three digits. For example, 3000 becomes '3,000' and 45000 becomes '45,000'.
	
* intword
	* Converts a large integer to a friendly text representation. Works best for numbers over 1 million. For example, 1000000 becomes '1.0 million', 1200000 becomes '1.2 million' and '1200000000' becomes '1.2 billion'.

* apnumber
	* For numbers 1-9, returns the number spelled out. Otherwise, returns the number. This follows Associated Press style.

* naturalday
	* For date values that are tomorrow, today or yesterday compared to present day returns representing string. Otherwise, returns a string formatted according to settings.DATE_FORMAT.

View Decorators
---------------

_None_

Forms
-----

_None_

Constants
---------

_None_
