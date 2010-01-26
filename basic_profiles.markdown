basic\_profiles
===============

_for pinax version 0.7.1_

Code for basic_profiles is online at [GitHub](http://github.com): [http://github.com/pinax/pinax/tree/0.7.1/pinax/apps/basic_profiles/](http://github.com/pinax/pinax/tree/0.7.1/pinax/apps/basic_profiles/)

Data Model
----------

* Dependencies: 
	* django.contrib.auth
	* notification (optional)
	
* Profile

	* user (foreign-key -> django.contrib.auth.models.User)
	* name (char 50)
	* about (text)
	* location (char 40)
	* website (url)


* Methods (basic_profiles.models...)

	* `create_profile(sender, instance=None, **kwargs)`
	
		creates a profile for the user, expecting "instance" to be a django.contrib.auth.models.User object
	
URL Design
----------

* `/profiles`

	`url(r'^username_autocomplete/$', 'autocomplete_app.views.username_autocomplete_all', name='profile_username_autocomplete'),
	url(r'^$', 'basic_profiles.views.profiles', name='profile_list'),
	url(r'^profile/(?P<username>[\w\._-]+)/$', 'basic_profiles.views.profile', name='profile_detail'),
	url(r'^edit/$', 'basic_profiles.views.profile_edit', name='profile_edit'),`

Views & Templates
-----------------

* `profiles(request, template_name="basic_profiles/profiles.html")`

	* default template: basic_profiles/profiles.html
	* context
		* users
		* order
		* search_terms

* `profile(request, username, template_name="basic_profiles/profile.html")`

	* default template: basic_profiles/profile.html
	* context
		* is_me
		* other_user

* `profile_edit(request, form_class=ProfileForm, **kwargs)`
	* uses @login_required
	
	* default template: basic_profiles/profile_edit.html
	* context
		* profile
		* profile_form

* Embedded Default Templates
	* _from basic\_profiles_
		* profile\_item.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/apps/basic_profiles/templates/profile_item.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/apps/basic_profiles/templates/profile_item.html)
		 
	* _from pinax_
		* basic_profiles/base.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/basic_profiles/base.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/basic_profiles/base.html)
		* basic_profiles/profile.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/basic_profiles/profile.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/basic_profiles/profile.html)
		* basic_profiles/profile\_edit.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/basic_profiles/profile_edit.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/basic_profiles/profile_edit.html)
		* basic_profiles/profile\_edit\_facebox.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/basic_profiles/profile_edit_facebox.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/basic_profiles/profile_edit_facebox.html)
		* basic_profiles/profile\_form.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/basic_profiles/profile_form.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/basic_profiles/profile_form.html)
		* basic_profiles/profile\_right\_panel.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/basic_profiles/profile_right_panel.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/basic_profiles/profile_right_panel.html)
		* basic_profiles/profiles.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/basic_profiles/profiles.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/basic_profiles/profiles.html)
	
TemplateTags
------------

* show\_profile
	* an inclusion tag that shows the profile of a user using the template "profile_item.html"
	* Example:

		`{% show_profile user %}`

* clear\_search\_url
	* renders a link that will clear the search terms, if any
	* Example:
	
		`{% if search_terms %}
            <a href="{% clear_search_url request %}">Clear Search Terms</a>
        {% endif %}`

Filters
-------

_None_

View Decorators
---------------

_None_

Forms
-----

* ProfileForm
	
	A form based on the Profile model, excluding the user foreign-key element

Constants
---------

_None_

