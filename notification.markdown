notification
============

_for notification version 0.1.4_

Code for django-notification is online at [GitHub](http://github.com): [http://github.com/jtauber/django-notification](http://github.com/jtauber/django-notification)

[Online usage documentation](http://github.com/jtauber/django-notification/blob/master/docs/usage.txt)

Data Model
----------

* Dependencies: 
	* django.contrib.sites
	* django.contrib.auth
	* django.contrib.contenttypes
	* mailer (optional - will fall back to using django.core.mail)
	
* NoticeType

	* label (char 40)
	* display (char 50
	* description (char 100)

* NoticeSetting

	* user (foreign-key -> django.contrib.auth.models.User)
	* notice_type (foreign-key -> NoticeType)
	* medium (char - choices NOTICE_MEDIA)
		* NOTICE_MEDIA
			* "1" : "Email"
		* NOTICE_MEDIA_DEFAULTS
			* "1" : 2
	* send (boolean)

	Indicates, for a given user, whether to send notifications
    of a given type to a given medium.

* Notice

	* user (foreign-key -> django.contrib.auth.models.User)
	* message (text)
	* notice_type (foreign-key -> NoticeType)
	* added (datetime)
	* unseen (boolean)
	* archived (boolean)
	* on_site (boolean)
	
	* Methods (NoticeManager) - User.objects...
	
		* `notices_for(self, user, archived=False, unseen=None, on_site=None)`
		
	        returns Notice objects for the given user.

	        If archived=False, it only include notices not archived.
	        If archived=True, it returns all notices for that user.

	        If unseen=None, it includes all notices.
	        If unseen=True, return only unseen notices.
	        If unseen=False, return only seen notices.
	
		* `unseen_count_for(self, user, **kwargs)`
		
			returns the number of unseen notices for the given user but does not
	        mark them seen
		
	* Methods - Notice...
	
		* is_unseen(self)
		
			returns value of self.unseen but also changes it to false.
	        Use this in a template to mark an unseen notice differently the first
	        time it is shown.

* NoticeQueueBatch

	A queued notice.
    Denormalized data for a notice.

	* pickled_data (text)

* ObservedItem

	* user (foreign-key -> django.contrib.auth.models.User)
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
	
	* `create_notice_type(label, display, description, default=2, verbosity=1)`

		Creates a new NoticeType.
	    This is intended to be used by other apps as a post_syncdb manangement step.
	
	* `get_notification_language(user)`
	
		Returns site-specific notification language for this user. Raises
	    LanguageStoreNotAvailable if this site does not use translated
	    notifications.
	
	* `get_formatted_messages(formats, label, context)`
	
		Returns a dictionary with the format identifier as the key. The values are
	    are fully rendered templates with the given context.
	
	* `send_now(users, label, extra_context=None, on_site=True)`
	
		Creates a new notice.

	    This is intended to be how other apps create new notices.

	    `notification.send(user, 'friends_invite_sent', {
	        'spam': 'eggs',
	        'foo': 'bar',
	    )`

	    You can pass in on_site=False to prevent the notice emitted from being
	    displayed on the site.

	* `send(*args, **kwargs)`

		A basic interface around both queue and send_now. This honors a global
		flag NOTIFICATION_QUEUE_ALL that helps determine whether all calls should
		be queued or not. A per call ``queue`` or ``now`` keyword argument can be
		used to always override the default global behavior.

	* `queue(users, label, extra_context=None, on_site=True)`
	
		Queue the notification in NoticeQueueBatch. This allows for large amounts
	    of user notifications to be deferred to a seperate process running outside
	    the webserver.
	
	* `observe(observed, observer, notice_type_label, signal='post_save')`
	
		Create a new ObservedItem.
	    To be used by applications to register a user as an observer for some object.

	* `stop_observing(observed, observer, signal='post_save')`
	
		Remove an observed item.
	
	* `send_observation_notices_for(observed, signal='post_save')`
	
		Send a notice for each registered user about an observed object.
		
	* `is_observing(observed, observer, signal='post_save')`
	
	* `handle_observations(sender, instance, *args, **kw)`
		
URL Design
----------

	url(r'^$', notices, name="notification_notices"),
	url(r'^(\d+)/$', single, name="notification_notice"),
	url(r'^feed/$', feed_for_user, name="notification_feed_for_user"),
	url(r'^mark_all_seen/$', mark_all_seen, name="notification_mark_all_seen"),

Views & Templates
-----------------

* `feed_for_user(request)`
	* uses: `@basic_auth_required(realm='Notices Feed', callback_func=simple_basic_auth_callback)`

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

* `archive(request, noticeid=None, next_page=None)`
	* uses `@login_required`

	* default template: _None_ always redirected

* `delete(request, noticeid=None, next_page=None)`
	* uses `@login_required`

	* default template: _None_ always redirected

* `mark_all_seen(request)`
	* uses `@login_required`

	* default template: _None_ always redirected

* Embedded Default Templates
	* _from django notification_
		* email_body.txt [http://github.com/jtauber/django-notification/blob/master/notification/templates/notification/email_body.txt](http://github.com/jtauber/django-notification/blob/master/notification/templates/notification/email_body.txt)
		* email_subject.txt [http://github.com/jtauber/django-notification/blob/master/notification/templates/notification/email_subject.txt](http://github.com/jtauber/django-notification/blob/master/notification/templates/notification/email_subject.txt)
		* full.html [http://github.com/jtauber/django-notification/blob/master/notification/templates/notification/full.html](http://github.com/jtauber/django-notification/blob/master/notification/templates/notification/full.html)
		* full.txt [http://github.com/jtauber/django-notification/blob/master/notification/templates/notification/full.txt](http://github.com/jtauber/django-notification/blob/master/notification/templates/notification/full.txt)
		* notice.html [http://github.com/jtauber/django-notification/blob/master/notification/templates/notification/notice.html](http://github.com/jtauber/django-notification/blob/master/notification/templates/notification/notice.html)
		* short.txt [http://github.com/jtauber/django-notification/blob/master/notification/templates/notification/short.txt](http://github.com/jtauber/django-notification/blob/master/notification/templates/notification/short.txt)

	* _from pinax_
		* notification/base.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/notification/base.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/notification/base.html)
		* notification/notices.html [http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/notification/notices.html](http://github.com/pinax/pinax/blob/0.7.1/pinax/templates/default/notification/notices.html)

	* _additional notice templates are included in other pinax applications_
	
View Decorators
---------------

* `simple_basic_auth_callback(request, user, *args, **kwargs)`

    Simple callback to automatically login the given user after a successful
    basic authentication.

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

_None_

Constants
---------

* VERSION
