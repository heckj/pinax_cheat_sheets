waitinglist
===========

_for pinax version 0.7.1_

Code for django-notification is online at [GitHub](http://github.com): [http://github.com/pinax/pinax/tree/0.7.1/pinax/apps/signup_codes](http://github.com/pinax/pinax/tree/0.7.1/pinax/apps/signup_codes)

Data Model
----------

* Dependencies: _None_
	
* WaitingListEntry

	* email (email)
	* created (datetime)
	
URL Design
----------

	url(r'^$', homepage, name="home"),
    url(r'^success/$', direct_to_template, {"template": "waitinglist/success.html"}, name="waitinglist_sucess"),

Views & Templates
-----------------

* Embedded Default Templates

	* _from pinax_
		* waitinglist/success.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/waitinglist/success.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/waitinglist/success.html)
	
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

* WaitingListEntryForm (from model WaitingListEntry)
	* email

	A form that adds an email address to the WaitingListEntry.

Constants
---------

_None_

