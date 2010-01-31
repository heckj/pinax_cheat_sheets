emailconfirmation
=================

_for emailconfiromation version 0.1.3_

Code for emailconfirmation is online at [GitHub](http://github.com): [http://github.com/jtauber/django-email-confirmation](http://github.com/jtauber/django-email-confirmation)

[Online usage documentation](http://github.com/jtauber/django-email-confirmation/blob/master/docs/index.txt)

Data Model
----------

* Dependencies: 
	* django.contrib.sites
	* django.contrib.auth
	
* EmailAddress

	* user (foreign-key -> django.contrib.auth.models.User)
	* email (email)
	* verified (boolean)
	* primary (boolean)
	
	* Methods (EmailAddressManager) - EmailAddress.objects...
	
		* `add_email(self, user, email)`

		* `get_primary(self, user)`

		* `get_users_for(self, email)`
		
			returns a list of users with the given email.
	
	* Methods - EmailAddress...
	
		* `set_as_primary(self, conditional=False)`

* EmailConfirmation

	* email_address (foreign-key -> EmailAddress)
	* sent (datetime)
	* confirmation_key (char 40)

	* Methods - EmailConfirmation...
	
		* `key_expired(self)`
		
			returns boolean true if time is past settings.EMAIL\_CONFIRMATION\_DAYS
	
		* Methods (EmailConfirmationManager) - EmailConfirmation.objects...

			* `confirm_email(self, confirmation_key)`
			
			* `send_confirmation(self, email_address)`
				* uses templates:
				 	* emailconfirmation/email\_confirmation\_subject.txt
					* emailconfirmation/email\_confirmation\_message.txt
			
			* `delete_expired_confirmations(self)`
	
URL Design
----------

_None_

Views & Templates
-----------------

* `confirm_email(request, confirmation_key)`

	* default template: emailconfirmation/confirm_email.html
	* context
		* email_address

* Embedded Default Templates
	* _from email\_notification_
		* emailconfirmation/email\_confirmation\_subject.txt [http://github.com/jtauber/django-email-confirmation/blob/master/emailconfirmation/templates/emailconfirmation/email\_confirmation\_subject.txt](http://github.com/jtauber/django-email-confirmation/blob/master/emailconfirmation/templates/emailconfirmation/email_confirmation_subject.txt)
		* emailconfirmation/email\_confirmation\_message.txt [http://github.com/jtauber/django-email-confirmation/blob/master/emailconfirmation/templates/emailconfirmation/email\_confirmation\_message.txt](http://github.com/jtauber/django-email-confirmation/blob/master/emailconfirmation/templates/emailconfirmation/email_confirmation_message.txt)

	* _from pinax_
		* emailconfirmation/confirm\_email.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/emailconfirmation/confirm\_email.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/emailconfirmation/confirm_email.html)
	
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

* settings.EMAIL\_CONFIRMATION\_DAYS
