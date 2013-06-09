django-choice-flow
==================

Meta Choice with simple flow and rules


Usage
======

```python
from django.db import models
from django_choices_flow import Choices
from django_choices_flow.models import FlowIntegerField


class MyChoices(Choices):
    NEW = 1, 'New content' # 'New content' is the display text
    WAIT = 2, 'Wait'
    CANCELED = -1, 'Canceled'
    ERROR = -2, 'Error'
    INVOICED = 3, 'Invoiced'

    # set transaction rules
    NEW_RULES = [NEW, INVOICED, CANCELED, ERROR]
    WAIT_RULES = [CANCELED, ERROR, INVOICED]
    INVOICED_RULES = [CANCELED]


class Invoces(models.Model):
	"""
	To use one choices
	"""
    number = models.IntegerField()
    status = models.IntegerField(choices=MyChoices, default=MyChoices.NEW)

    def __unicode__(self):
        return self.number
        

class FlowInvoice(models.Model):
	"""
	To validate flow in choices
	"""

	number = models.IntegerField()
	status = FlowIntegerField(choices=MyChoices, default=MyChoices.NEW)
	
	def __unicode__(self):
        return self.number

```

