account
=======

_for pinax 0.7.1_

Code for pinax is online at [GitHub](http://github.com): [http://github.com/pinax/pinax/tree/0.7.1/](http://github.com/pinax/pinax/tree/0.7.1/)

Data Model
----------

* Dependencies: 
	* django.contrib.auth
	* emailconfirmation
	* timezones
	
* Account

	* user (foreign-key -> django.contrib.auth.models.User)
	* timezone (timezone)
	* language (char 10, choices settings.LANGUAGES)

* OtherServiceInfo

	* user (foreign-key -> django.contrib.auth.models.User)
	* key (char 50)
	* value (text)

* PasswordReset

	* user (foreign-key -> django.contrib.auth.models.User)
	* temp_key (char 100)
	* timestamp (datetime)
	* reset (boolean)
	

* Methods (account.models...)

	* `other_service(user, key, default_value="")`
	
		retrieve the other service info for given key for the given user.
	    return default_value ("") if no value.

	* `update_other_services(user, **kwargs)`
	
		update the other service info for the given user using the given keyword args.
	    e.g. update_other_services(user, twitter\_user=..., twitter\_password=...)
	
	* `create_account(sender, instance=None, **kwargs)`
	
		creates an account, where instance is a django.contrib.auth.models.User instance

	* `superuser_email_address(sender, instance=None, **kwargs)`
	
		only used in syncdb or createsuperuser to associate an email with the super user

	* `mark_user_active(sender, instance=None, **kwargs)`
	
		triggered from a signal "email_confirmed" to mark user as active

URL Design
----------

* /account

`   
	url(r'^email/$', 'account.views.email', name="acct_email"),
    url(r'^signup/$', 'account.views.signup', name="acct_signup"),
    url(r'^login/$', 'account.views.login', name="acct_login"),
    url(r'^login/openid/$', 'account.views.login', {'associate_openid': True},
        name="acct_login_openid"),
    url(r'^password_change/$', 'account.views.password_change', name="acct_passwd"),
    url(r'^password_set/$', 'account.views.password_set', name="acct_passwd_set"),
    url(r'^password_delete/$', 'account.views.password_delete', name="acct_passwd_delete"),
    url(r'^password_delete/done/$', 'django.views.generic.simple.direct_to_template', {
        "template": "account/password_delete_done.html",
    }, name="acct_passwd_delete_done"),
    url(r'^password_reset/$', 'account.views.password_reset', name="acct_passwd_reset"),
    url(r'^timezone/$', 'account.views.timezone_change', name="acct_timezone_change"),
    url(r'^other_services/$', 'account.views.other_services', name="acct_other_services"),
    url(r'^other_services/remove/$', 'account.views.other_services_remove', name="acct_other_services_remove"),
    url(r'^language/$', 'account.views.language_change', name="acct_language_change"),
    url(r'^logout/$', 'django.contrib.auth.views.logout', {"template_name": "account/logout.html"}, name="acct_logout"),
    url(r'^confirm_email/(\w+)/$', 'emailconfirmation.views.confirm_email', name="acct_confirm_email"),
    # Setting the permanent password after getting a key by email
    url(r'^password_reset_key/(\w+)/$', 'account.views.password_reset_from_key', name="acct_passwd_reset_key"),
    # ajax validation
    (r'^validate/$', 'ajax_validation.views.validate', {'form_class': SignupForm}, 'signup_form_validate'),`

Views & Templates
-----------------

* `login(request, form_class=LoginForm, template_name="account/login.html",
          success_url=None, associate_openid=False, openid_success_url=None,
          url_required=False, extra_context=None)`

	* default template: account/login.html
	* context
		* form
		* url_required

* `signup(request, form_class=SignupForm, template_name="account/signup.html", success_url=None)`
	
	* default template: account/signup.html
	* context:
		* form

* `email(request, form_class=AddEmailForm, template_name="account/email.html")`
	* uses `@login_required`

	* default template: account/email.html
	* context:
		* add\_email\_form

* `password_change(request, form_class=ChangePasswordForm,
		        template_name="account/password_change.html")`
	* uses `@login_required`

	* default template: account/password_change.html
	* context:
		* password\_change\_form

* `password_set(request, form_class=SetPasswordForm,
		        template_name="account/password_set.html")`
	* uses `@login_required`

	* default template: account/password_change.html
	* context:
		* password\_set\_form

* `password_delete(request, template_name="account/password_delete.html")`
	* uses `@login_required`
	
	* default template: account/password_delete.html

* `password_reset(request, form_class=ResetPasswordForm,
	        template_name="account/password_reset.html",
	        template_name_done="account/password_reset_done.html")`
	
	* default template: account/password_reset_done.html
	* context:
		* email OR password\_reset\_form

* `password_reset_from_key(request, key, form_class=ResetPasswordKeyForm,
		        template_name="account/password_reset_from_key.html")`

	* default template: account/password_reset_from_key.html
	* context:
		* form

* `timezone_change(request, form_class=ChangeTimezoneForm,
		        template_name="account/timezone_change.html")`
	* uses `@login_required`

	* default template: account/timezone_change.html
	* context:
		* form

* `language_change(request, form_class=ChangeLanguageForm,
		        template_name="account/language_change.html")`
	* uses `@login_required`

	* default template: account/language_change.html
	* context:
		* form

* `other_services(request, template_name="account/other_services.html")`
	* uses `@login_required`

	* default template: account/language_change.html
	* context:
		* twitter_form
		* twitter_authorized

* `other_services_remove(request)`
	* uses `@login_required`

* Embedded Default Templates
	* _from pinax_
		* account/base.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/base.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/base.html)
		* account/email.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/email.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/email.html)
		* account/language_change.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/language_change.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/language_change.html)
		* account/login.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/login.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/login.html)
		* account/logout.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/logout.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/logout.html)
		* account/password\_change.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/password_change.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/password_change.html)
		* account/password\_delete.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/password_delete.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/password_delete.html)
		* account/password\_delete\_done.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/password_delete_done.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/password_delete_done.html)
		* account/password\_reset.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/password_reset.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/password_reset.html)
		* account/password\_reset\_done.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/password_reset_done.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/password_reset_done.html)
		* account/password\_reset\_from_key.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/password_reset_from_key.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/password_reset_from_key.html)
		* account/password\_reset\_key\_message.txt [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/password_reset_key_message.txt](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/password_reset_key_message.txt)
		* account/password\_reset\_message.txt [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/password_reset_message.txt](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/password_reset_message.txt)
		* account/password\_sent.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/password_set.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/password_set.html)
		* account/signup.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/signup.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/signup.html)
		* account/timzone\_change.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/timezone_change.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/timezone_change.html)
		* account/verification_sent.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/verification_sent.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/account/verification_sent.html)

	
TemplateTags
------------

* openid_icon
	* renders an openid icon
	* Example:

		`{% openid_icon openid user %}<b>{{ user }}</b>`

* other_service
	* Example:
	
		`{% other_service user key %}`
		`{% other_service user key as var %}`

Filters
-------

_None_

View Decorators
---------------

_None_

Forms
-----

* LoginForm
	* username
	* password1
	* remember
	
* SignupForm
	* username
	* password1
	* password2
	
* OpenIDSignupForm
	* username
	* email (if settings.ACCOUNT\_REQUIRED\_EMAIL or settings.ACCOUNT\_EMAIL\_VERIFICATION)

* UserForm
	
* AccountForm

* AddEmailForm
	* email
	
* ChangePasswordForm
	* oldpassword
	* password1
	* password2

* SetPasswordForm
	* password1
	* password2

* ResetPasswordForm
	* email

* ResetPasswordKeyForm
	* password1
	* password2
	* temp_key

* ChangeTimezoneForm

* ChangeLanguageForm

* TwitterForm
	* username
	* password

ContextProcessor
----------------

* site\_wide\_announcements

	Adds the site-wide announcements to the global context of templates.


Constants
---------

* settings.LOGIN\_REDIRECT\_URLNAME