signup_codes
============

_for pinax 0.7.1_

Code for django-notification is online at [GitHub](http://github.com): [http://github.com/pinax/pinax/tree/0.7.1/pinax/apps/signup_codes](http://github.com/pinax/pinax/tree/0.7.1/pinax/apps/signup_codes)

Data Model
----------

* Dependencies: 
	* django.contrib.auth
	* account
	
* SignupCode

	* code (char 40)
	* max\_uses (int)
	* expiry (datetime)
	* inviter (foreign-key -> django.contrib.auth.models.User)
	* email (email)
	* notes (text)
	* created (datetime)
	* use\_count (int) _calculated_

	* Methods - SignupCode...
	
		* `calculate_use_count(self)`
		
		* `use(self, user)`
		
			Add a SignupCode result attached to the given user.

* SignupCodeResult

	* signup\_code (foreign-key -> SignupCode)
	* user (foreign-key -> django.contrib.auth.models.User)
	* timestamp (datetime)

* Methods (signup_code.models...)

	* `check_signup_code(code)`
	
		returns a boolean if the signup code is valid
	
URL Design
----------

    url(r'^admin/invite_user/$', 'signup_codes.views.admin_invite_user', name="admin_invite_user"),
    url(r'^account/signup/$', signup_view, name="acct_signup"),

Views & Templates
-----------------

* `signup(request, form_class=SignupForm,
        template_name="account/signup.html", success_url=None)`

	* default template: account/signup.html
	* context
		* code
		* form

* `admin_invite_user(request, form_class=InviteUserForm,
		        template_name="signup_codes/admin_invite_user.html")`
	* uses `@staff_member_required`
	
	This view, by default, works inside the Django admin.
	
	* default template: signup\_codes/admin\_invite\_user.html
	* context:
		* title
		* form

* Embedded Default Templates
	* _from pinax_
		* signup\_codes/admin\_invite\_user.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/signup_codes/admin_invite_user.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/signup_codes/admin_invite_user.html)
		* signup\_codes/failure.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/signup_codes/failure.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/signup_codes/failure.html)
		* signup\_codes/invite\_user.txt [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/signup_codes/invite_user.txt](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/signup_codes/invite_user.txt)

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

* SignupForm (account.SignupForm)
	* signup_code

* InviteUserForm
	* email

Constants
---------

* settings.ACCOUNT\_OPEN\_SIGNUP
