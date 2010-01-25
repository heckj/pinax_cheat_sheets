mailer
======

_for mailer version 0.1.1_

Code for django-notification is online at [GitHub](http://github.com): [http://github.com/jtauber/django-mailer/](http://github.com/jtauber/django-mailer/)

[Online usage documentation](http://github.com/jtauber/django-mailer/blob/master/docs/usage.txt)

Data Model
----------

* Dependencies: _None_
	
* NoticeType

	* label (char 40)
	* display (char 50
	* description (char 100)

* ObservedItem

	* user (foreign-key -> django.contrib.auth.User)
	* content_type (foreign-key -> django.contrib.contenttypes.ContentType)
	* observed_object (foreign-key -> django.contrib.contenttypes.GenericForeignKey)
	* notice_type (foreign-key -> NoticeType)
	* added (datetime)
	* signal (text)
	
	* Methods (ObservedItemManager) - ObservedItem.objects...
	
		* `all_for(self, observed, signal)`
		
		Returns all ObservedItems for an observed object,
        to be sent when a signal is emited.

		* `get_for(self, observed, observer, signal)`
	
	* Methods - ObservedItem...
	
		* `send_notice(self)`

* Methods (notification.models...)

	* `get_notification_setting(user, notice_type, medium)`
	
		gets or creates a notification setting to return

	* `should_send(user, notice_type, medium)`
	
		returns bool from user's notification setting
	
URL Design
----------

	url(r'^$', notices, name="notification_notices"),
	url(r'^(\d+)/$', single, name="notification_notice"),
	url(r'^feed/$', feed_for_user, name="notification_feed_for_user"),
	url(r'^mark_all_seen/$', mark_all_seen, name="notification_mark_all_seen"),

Views & Templates
-----------------

* `notices(request)`
	* uses `@login_required`

	* default template: notification/notices.html
	* context
		* notices
		* notice_types
		* notice_settings

* `single(request, id)`
	* uses `@login_required`
	
	* default template: notification/single.html
	* context:
		* notice

* Embedded Default Templates
	* _from django notification_
		* email_body.txt [http://github.com/jtauber/django-notification/blob/master/notification/templates/notification/email_body.txt](http://github.com/jtauber/django-notification/blob/master/notification/templates/notification/email_body.txt)

	* _from pinax_
		* notification/notices.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/notification/notices.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/notification/notices.html)

	* _additional notice templates are included in other pinax applications_
	
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

View Decorators
---------------

* `basic_auth_required(realm=None, test_func=None, callback_func=None)`

    This decorator should be used with views that need simple authentication
    against Django's authentication framework.
    
    The ``realm`` string is shown during the basic auth query.
    
    It takes a ``test_func`` argument that is used to validate the given
    credentials and return the decorated function if successful.
    
    If unsuccessful the decorator will try to authenticate and checks if the
    user has the ``is_active`` field set to True.
    
    In case of a successful authentication  the ``callback_func`` will be
    called by passing the ``request`` and the ``user`` object. After that the
    actual view function will be called.
    
    If all of the above fails a "Authorization Required" message will be shown.

Forms
-----

* UserCreationForm
	* username
	* password1
	* password2
	
	A form that creates a user, with no privileges, from the given username and password.

Constants
---------

* VERSION
