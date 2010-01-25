django.contrib.sessions
=======================

_for Django version 1.1_

Data Model
----------

Dependency: _None_

* Session

	* session_key (char 40)
	* session_data (text)
	* expire_date (datetime)

    Django provides full support for anonymous sessions. The session
    framework lets you store and retrieve arbitrary data on a
    per-site-visitor basis. It stores data on the server side and
    abstracts the sending and receiving of cookies. Cookies contain a
    session ID -- not the data itself.

    The Django sessions framework is entirely cookie-based. It does
    not fall back to putting session IDs in URLs. This is an intentional
    design decision. Not only does that behavior make URLs ugly, it makes
    your site vulnerable to session-ID theft via the "Referer" header.

    For complete documentation on using Sessions in your code, consult
    the sessions documentation that is shipped with Django (also available
    on the Django website).

	* Methods (SessionManager) - Session.objects...
	
		* `encode(self, session_dict)`
		
	        Returns the given session dictionary pickled and encoded as a string.
	
		* `save(self, session_key, session_dict, expire_date)`
		
			Saves session data, or deletes all session data is session_dict is None
		
	* Methods - Session...
	
		* get_decoded() - returns decoded session dictionary

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

_None_
