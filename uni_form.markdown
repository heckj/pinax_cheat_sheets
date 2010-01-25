uni_form
========

_for uni_form version 0.6.0_

Code for django-notification is online at [GitHub](http://github.com): [http://github.com/pydanny/django-uni-form/tree/0.6.0](http://github.com/pydanny/django-uni-form/tree/0.6.0)

[Online usage documentation](http://github.com/pydanny/django-uni-form/blob/0.6.0/docs/usage.txt) and [README](http://github.com/pydanny/django-uni-form/blob/0.6.0/README.rst)

Data Model
----------

_None_
	
URL Design
----------

_None_

Views & Templates
-----------------

In your views.py add the following after field definitions:

`from django.shortcuts import render_to_response

from uni_form.helpers import FormHelper, Submit, Reset
from my_project.forms.MyForm

def my_view(request):

    # Create the form
    form = MyForm()

    # create a formHelper
    helper = FormHelper()

    # Add in a class and id
    helper.form_id = 'this-form-rocks'
    helper.form_class = 'search'

    # add in a submit and reset button
    submit = Submit('search','search this site')
    helper.add_input(submit)
    reset = Reset('reset','reset button')
    helper.add_input(reset)

    # create the response dictionary
    response_dictionary = {'form':form, 'helper': helper}

    return render_to_response('my_template.html', response_dictionary)
`

* _from uni\_form_
	* uni\_form/errors.html [http://github.com/pydanny/django-uni-form/blob/0.6.0/uni\_form/templates/uni\_form/errors.html](http://github.com/pydanny/django-uni-form/blob/0.6.0/uni_form/templates/uni_form/errors.html)
	* uni\_form/field.html [http://github.com/pydanny/django-uni-form/blob/0.6.0/uni\_form/templates/uni\_form/field.html](http://github.com/pydanny/django-uni-form/blob/0.6.0/uni_form/templates/uni_form/field.html)
	* uni\_form/uni\_form.html [http://github.com/pydanny/django-uni-form/blob/0.6.0/uni\_form/templates/uni\_form/uni_form.html](http://github.com/pydanny/django-uni-form/blob/0.6.0/uni_form/templates/uni_form/uni_form.html)
	* uni\_form/uni\_form\_jquery.html [http://github.com/pydanny/django-uni-form/blob/0.6.0/uni\_form/templates/uni\_form/uni_form_jquery.html](http://github.com/pydanny/django-uni-form/blob/0.6.0/uni_form/templates/uni_form/uni_form_jquery.html)
	* uni\_form/whole\_uni\_form.html [http://github.com/pydanny/django-uni-form/blob/0.6.0/uni\_form/templates/uni\_form/whole_uni_form.html](http://github.com/pydanny/django-uni-form/blob/0.6.0/uni_form/templates/uni_form/whole_uni_form.html)
	
TemplateTags
------------

* do_uni_form
	* You need to pass in at least the form object, and can also pass in the
    optional attrs string. Writing the attrs string is rather challenging so
    use of the objects found in uni_form.helpers is encouraged.
    
    form: The forms object to be rendered by the tag
    
    attrs (optional): A string of semi-colon seperated attributes that can be
    applied to theform in string format. They are used as follows.
    
    form_action: applied to the form action attribute. Must be a named url in your urlconf that can be executed via the *url* default template tag. Defaults to empty::
        
        form_action=<my-form-action>
    
    form_method: applied to the form action attribute. Defaults to POST and the only available thing you can enter is GET.::
        
        form_method=<my-form-method>
    
    id: applied to the form as a whole. Defaults to empty::
        
        id=<my-form-id>
    
    class: add space seperated classes to the class list. Always starts with uniform::
        
        class=<my-first-custom-form-class> <my-custom-form-class>
    
    button: for adding of generic buttons. The name also becomes the slugified id::
        
        button=<my-custom-button-name>|<my-custom-button-value>
    
    submit: For adding of submt buttons. The name also becomes the slugified id::
        
        submit=<my-custom-submit-name>|<my-custom-submit-value>
    
    hidden: For adding of hidden buttons::
        
        hidden=<my-custom-hidden-name>|<my-custom-hidden-value>
    
    reset: For adding of reset buttons::
        
        reset=<my-custom-reset-name>|<my-custom-reset-value>
        
        
	* Example:

		`{% uni_form my-form my_helper %}`

* uni_form_jquery

Filters
-------

* as_uni_form
* as_uni_errors
* as_uni_field

	`{% load uni_form %}
	{% uni_form form helper %}`

View Decorators
---------------

_None_

Forms
-----

_None_

Constants
---------

* VERSION
