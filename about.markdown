about
=====

_for pinax version 0.7.1_

Code for pinax is online at [GitHub](http://github.com): [http://github.com/pinax/pinax/tree/0.7.1/](http://github.com/pinax/pinax/tree/0.7.1/)

Data Model
----------

* Dependencies: _None_

_None_
	
URL Design
----------

* `/about/`

	`url(r'^$', direct_to_template, {"template": "about/about.html"}, name="about"),
	url(r'^terms/$', direct_to_template, {"template": "about/terms.html"}, name="terms"),
	url(r'^privacy/$', direct_to_template, {"template": "about/privacy.html"}, name="privacy"),
	url(r'^dmca/$', direct_to_template, {"template": "about/dmca.html"}, name="dmca"),
	url(r'^what_next/$', direct_to_template, {"template": "about/what_next.html"}, name="what_next"),`

Views & Templates
-----------------

_None_

* Embedded Default Templates
	* _from pinax_
		* about/about.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/about/about.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/about/about.html)
		* about/dmca.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/about/dmca.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/about/dmca.html)
		* about/privacy.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/about/privacy.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/about/privacy.html)
		* about/terms.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/about/terms.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/about/terms.html)

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

_None_
