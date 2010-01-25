django\_openid
=============

_for django\_openid version 0.2.0_

Code for django\_openid is online at [GitHub](http://github.com): [http://github.com/brosner/django-openid/](http://github.com/brosner/django-openid/)

[Online usage documentation](http://github.com/brosner/django-openid/tree/master/django_openid/docs/)

* [Integrating with django.contrib.auth](http://github.com/brosner/django-openid/blob/master/django_openid/docs/auth-integration.txt
)
Data Model
----------

* Dependencies: 
	* django.contrib.auth (optional)
	
* Nonce

	* server_url (char 255)
	* timestamp (int)
	* sale (char 40)

* Association

	* server_url (text 2047)
	* handle (char 255)
	* secret (char 255)
	* issued (int)
	* lifetime (int)
	* assoc_type (text 64)

* UserOpenidAssociation

	* user (foreign-key -> django.contrib.auth.User)
	* openid (char 255)
	* created (datetime)
	
URL Design
----------

	(r'^openid/(.*)', PinaxConsumer()) - used with "account" in Pinax project

Views & Templates
-----------------

* Embedded Default Templates
	* _from django\_openid_
		* django\_openid/register\_form\_field.html [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/_register_form_field.html](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/_register_form_field.html)
		* django\_openid/admin\_login.html [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/admin_login.html](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/admin_login.html)
		* django\_openid/already\_logged\_in.html [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/already_logged_in.html](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/already_logged_in.html)
		* django\_openid/associate.html [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/associate.html](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/associate.html)
		* django\_openid/associations.html [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/associations.html](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/associations.html)
		* django\_openid/base.html [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/base.html](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/base.html)
		* django\_openid/decide.html [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/decide.html](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/decide.html)
		* django\_openid/error.html [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/error.html](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/error.html)
		* django\_openid/landing\_page.html [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/landing\_page.html](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/landing_page.html)
		* django\_openid/login.html [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/login.html](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/login.html)
		* django\_openid/login\_plus\_password.html [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/login\_plus\_password.html](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/login_plus_password.html)
		* django\_openid/message.html [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/message.html](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/message.html)
		* django\_openid/pick\_account.html [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/pick\_account.html](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/pick_account.html)
		* django\_openid/recover.html [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/recover.html](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/recover.html)
		* django\_openid/recovery\_complete.html [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/recovery\_complete.html](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/recovery_complete.html)
		* django\_openid/recovery\_email.txt [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/recovery\_email.txt](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/recovery_email.txt)
		* django\_openid/recovery\_expired.html [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/recovery\_expired.html](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/recovery_expired.html)
		* django\_openid/register.html [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/register.html](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/register.html)
		* django\_openid/register\_complete.html [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/register\_complete.html](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/register_complete.html)
		* django\_openid/register\_confirm\_email.txt [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/register\_confirm\_email.txt](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/register_confirm_email.txt)
		* django\_openid/register\_sent\_email.html [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/register\_email\_sent.html](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/register_email_sent.html)
		* django\_openid/set\_password.html [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/set\_password.html](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/set_password.html)
		* django\_openid/this\_is\_an\_openid\_server.html [http://github.com/brosner/django-openid/blob/master/django\_openid/templates/django\_openid/this\_is\_an\_openid\_server.html](http://github.com/brosner/django-openid/blob/master/django_openid/templates/django_openid/this_is_an_openid_server.html)
		
	
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
