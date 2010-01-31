mailer
======

_for mailer version 0.1.1_

Code for mailer is online at [GitHub](http://github.com): [http://github.com/jtauber/django-mailer/](http://github.com/jtauber/django-mailer/)

[Online usage documentation](http://github.com/jtauber/django-mailer/blob/master/docs/usage.txt)

Data Model
----------

* Dependencies: _None_
	
* Message

	* to_address (char 50)
	* from_address (char 50)
	* subject (char 100)
	* message_body (text)
	* when_added (datetime)
	* priority (char - choices of PRIORITIES)
		* '1' : 'high'
		* '2' : 'medium'
		* '3' : 'low'
		* '4' : 'deferred'
	
	* Methods (MessageManager) - Message.objects...
	
		* `high_priority(self)`
		
		the high priority messages in the queue

		* `medium_priority(self)`
		
		the medium priority messages in the queue
		
		* `low_priority(self)`
		
		the low priority messages in the queue

		* `non_deferred(self)`
		
		the messages in the queue not deferred
		
		* `deferred(self)`
		
		the deferred messages in the queue
		
		* `retry_deferred(self, new_priority=2)`
	
	* Methods - Message...
	
		* `defer(self)`
	
		* `retry(self, new_priority=2)`

* DontSendEntry

	* to_address (char 50)
	* when_added (datetime)

	* Methods (DontSendEntryManager) - DontSendEntry.objects...
	
		* `has_address(self, address)`
		
		is the given address on the don't send list?


* MessageLog

	* to_address (char 50)
	* from_address (char 50)
	* subject (char 100)
	* message_body (text)
	* when_added (datetime)
	* priority (char - choices PRIORITIES)
	* when_attempted (datetime)
	* result (char - choices RESULT_CODES)
		* RESULT_CODES
			* '1' : 'success'
			* '2' : 'don\'t send'
			* '3' : 'failure'
	* log_message (text)
	
	* Methods (MessageLogManager) - MessageLog.objects...
	
		* `log(self, message, result_code, log_message = '')`
		
		create a log entry for an attempt to send the given message and
        record the given result and (optionally) a log message

URL Design
----------

_None_

Views & Templates
-----------------

_None_
	
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

* VERSION
* PRIORITY_MAPPING
	* "high": "1"
	* "medium": "2"
	* "low": "3"
	* "deferred": "4"
* settings.EMAIL\_SUBJECT\_PREFIX
* settings.SERVER\_EMAIL

Methods
-------

* `send_mail(subject, message, from_email, recipient_list, priority="medium",
              fail_silently=False, auth_user=None, auth_password=None)`

* `mail_admins(subject, message, fail_silently=False, priority="medium")`

* `mail_managers(subject, message, fail_silently=False, priority="medium")`