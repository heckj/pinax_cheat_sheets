django.contrib.contenttypes
===================

_for Django version 1.1_

Data Model
----------

* ContentType

	* name (char 100)
	* app_label (char 100)
	* model (char 100) - python model class name

	* Methods (ContentTypeManager) - ContentType.objects...
	
		* get_for_model(self, model):

	        Returns the ContentType object for a given model, creating the
	        ContentType if necessary. Lookups are cached so that subsequent lookups
	        for the same model don't hit the database.

		* get_for_id(self, id):

	        Lookup a ContentType by ID. Uses the same shared cache as get_for_model
	        (though ContentTypes are obviously not created on-the-fly by get_by_id).

		* clear_cache(self):

	        Clear out the content-type cache. This needs to happen during database
	        flushes to prevent caching of "stale" content type IDs (see
	        django.contrib.contenttypes.management.update_contenttypes for where
	        this gets called).		

	* Methods - ContentType...
		* model_class(self):
		
	        Returns the Python model class for this type of content
	
		* get_object_for_this_type(self, **kwargs):
		
	        Returns an object of this type for the keyword arguments given.
	        Basically, this is a proxy around this object_type's get_object() model
	        method. The ObjectNotExist exception, if thrown, will not be caught,
	        so code that calls this method should catch it.
	

URL Design
----------

_None_

Views & Templates
-----------------

* `shortcut(request, content_type_id, object_id)`

    Redirect to an object's page based on a content-type ID and an object ID.

