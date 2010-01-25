django.contrib.auth
===================

_for Django version 1.1_

Data Model
----------

Dependency: django.contrib.contenttypes

* Permission

	* name (char 50)
	* content_type (foreign key-> ContentType)
	* codename (char 100)

	The permissions system provides a way to assign permissions to specific users and groups of users.

    The permission system is used by the Django admin site, but may also be useful in your own code. The Django admin site uses permissions as follows:

        - The "add" permission limits the user's ability to view the "add" form and add an object.
        - The "change" permission limits a user's ability to view the change list, view the "change" form and change an object.
        - The "delete" permission limits the ability to delete an object.

    Permissions are set globally per type of object, not per specific object instance. It is possible to say "Mary may change news stories," but it's not currently possible to say "Mary may change news stories, but only the ones she created herself" or "Mary may only change news stories that have a certain status or publication date."

    Three basic permissions -- add, change and delete -- are automatically created for each Django model.
    

* Group

	* name (char 80)
	* permissions (many-to-many -> permission)

	Groups are a generic way of categorizing users to apply permissions, or some other label, to those users. A user can belong to any number of groups.

    A user in a group automatically has all the permissions granted to that group. For example, if the group Site editors has the permission can_edit_home_page, any user in that group will have that permission.

    Beyond permissions, groups are a convenient way to categorize users to apply some label, or extended functionality, to them. For example, you could create a group 'Special users', and you could write code that would do special things to those users -- such as giving them access to a members-only portion of your site, or sending them members-only e-mail messages.
	
* User

	* username (char 30)
	* first_name (char 30)
	* last_name (char 30)
	* email (email)
	* password (char 128)
	* is_staff (bool)
	* is_active (bool)
	* is_superuser (bool)
	* last_login (datetime)
	* date_joined (datetime)
	* groups (many-to-many -> groups)
	* user_permissions (many-to-many -> permission)

	Users within the Django authentication system are represented by this model.

	Username and password are required. Other fields are optional.

	* Methods (UserManager) - User.objects...
	
		* create_user(self, username, email, password=None):
		
	        "Creates and saves a User with the given username, e-mail and password."
	
		* create_superuser(self, username, email, password):
		
		* make_random_password(self, length=10, allowed_chars='abcdefghjkmnpqrstuvwxyzABCDEFGHJKLMNPQRSTUVWXYZ23456789'):
		
	        "Generates a random password with the given length and given allowed_chars"
	
	* Methods - User...
	
		* get_absolute_url() - returns "/users/..."
		* is_anonymous() - returns bool
		* is_authenticated() - returns bool
		* get_full_name() - returns "first_name last_name"
		* set_password(plaintext password) - sets a new password
		* check_password(plaintext password) - returns bool (if matched)
		* set_unusable_password() - sets an invalid password that will never match
		* has_usable_password() - bool no if set to unusuable through method call
		* get_group_permissions() - returns permission list
		* get_all_permissions() - returns permission list
		* has_perm(permission) - boolean if valid permission exists
		* has_perms(permission list) - boolean if valid permissions exist
		* has_module_perms(app_label) - boolean if permission in app label
		* get_and_delete_message() - returns list of messages accumulated
		* email_user(subject,message,from_email=None) - sends user an email
		* get_profile() - returns site-specific profile for user. Raises SiteProfileNotAvailable if this site does not allow profiles.

* Message

	* user (foreignkey -> User)
	* message (text)

URL Design
----------

	(r'^login/$', 'django.contrib.auth.views.login'),
	(r'^logout/$', 'django.contrib.auth.views.logout'),
	(r'^password_change/$', 'django.contrib.auth.views.password_change'),
	(r'^password_change/done/$', 'django.contrib.auth.views.password_change_done'),
	(r'^password_reset/$', 'django.contrib.auth.views.password_reset'),
	(r'^password_reset/done/$', 'django.contrib.auth.views.password_reset_done'),
	(r'^reset/(?P<uidb36>[0-9A-Za-z]+)-(?P<token>.+)/$', 'django.contrib.auth.views.password_reset_confirm'),
	(r'^reset/done/$', 'django.contrib.auth.views.password_reset_complete'),

Views & Templates
-----------------

* `login(request, template_name='registration/login.html', redirect_field_name=REDIRECT_FIELD_NAME)`

	Displays the login form and handles the login action.

	* default template: registration/login.html
	* context
		* form
		* site
		* site_name

* `logout(request, next_page=None, template_name='registration/logged_out.html', redirect_field_name=REDIRECT_FIELD_NAME)`

	Logs out the user and displays 'You are logged out' message.

	* default template: registration/logout.html
	* context if not redirected
		* title

* `logout_then_login(request, login_url=None)`

	Logs out the user if he is logged in. Then redirects to the log-in page.

* `redirect_to_login(next, login_url=None, redirect_field_name=REDIRECT_FIELD_NAME)`

	Redirects the user to the login page, passing the given 'next' page

* `password_reset(request, is_admin_site=False, template_name='registration/password_reset_form.html',
	        email_template_name='registration/password_reset_email.html',
	        password_reset_form=PasswordResetForm, token_generator=default_token_generator,
	        post_reset_redirect=None)`
	
	Sends password reset mail

	* default template: registration/password_reset_form.html
	* context if not redirected
		* form

* `password_reset_done(request, template_name='registration/password_reset_done.html')`
		"shows a success message for password reset"

	* default template: registration/password_reset_done.html

* `password_reset_confirm(request, uidb36=None, token=None, template_name='registration/password_reset_confirm.html',
                         token_generator=default_token_generator, set_password_form=SetPasswordForm,
                         post_reset_redirect=None)`

    View that checks the hash in a password reset link and presents a
    form for entering a new password.

	* default template: registration/password_reset_confirm.html
	* context if not redirected
		* validlink
		* form

* `password_reset_complete(request, template_name='registration/password_reset_complete.html')`

	* default template: registration/password_reset_complete.html
	* context 
		* login_url

* `password_change(request, template_name='registration/password_change_form.html',
	                    post_change_redirect=None)`

	* default template: registration/password_change_form.html

* `password_change_done(request, template_name='registration/password_change_done.html')`

	* default template: registration/password_change_done.html

View Decorators
---------------

* `user_passes_test(test_func, login_url=None, redirect_field_name=REDIRECT_FIELD_NAME)`

    Decorator for views that checks that the user passes the given test,
    redirecting to the log-in page if necessary. The test should be a callable
    that takes the user object and returns True if the user passes.

* `login_required(function=None, redirect_field_name=REDIRECT_FIELD_NAME)`

    Decorator for views that checks that the user is logged in, redirecting
    to the log-in page if necessary.

* `permission_required(perm, login_url=None)`

    Decorator for views that checks whether a user has a particular permission
    enabled, redirecting to the log-in page if necessary.

Forms
-----

* UserCreationForm
	* username
	* password1
	* password2
	
	A form that creates a user, with no privileges, from the given username and password.

* AuthenticationForm
	* username
	* password
	
	Base class for authenticating users. Extend this to get a form that accepts
    username/password logins.

* PasswordResetForm
	* email
	
	Validates that a user exists with the given e-mail address. Generates a one-use only link for resetting password and sends to the user.

* SetPasswordForm
	* newpassword1
	* newpassword2
	
	A form that lets a user change set his/her password without entering the old password

* PasswordChangeForm
	* old_password
	
	A form that lets a user change his/her password by entering their old password.

* AdminPasswordChangeForm
	* password1
	* password2
	
	A form used to change the password of a user in the admin interface.


Constants
---------

* SESSION_KEY = '_auth_user_id'
* BACKEND_SESSION_KEY = '_auth_user_backend'
* REDIRECT_FIELD_NAME = 'next'
