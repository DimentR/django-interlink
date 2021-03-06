===============================
Django-interlink
===============================


.. image:: https://badge.fury.io/py/django-interlink.svg
        :target: https://pypi.python.org/pypi/django-interlink

.. image:: https://img.shields.io/travis/alexmorozov/django-interlink.svg
        :target: https://travis-ci.org/alexmorozov/django-interlink

.. image:: https://readthedocs.org/projects/django-interlink/badge/?version=latest
        :target: https://django-interlink.readthedocs.io/en/latest/?badge=latest
        :alt: Documentation Status

.. image:: https://requires.io/github/alexmorozov/django-interlink/requirements.svg?branch=master
        :target: https://requires.io/github/alexmorozov/django-interlink/requirements?branch=master
        :alt: Dependencies


Boost your website's search engine rankings and usability by creating rich
internal links blocks.


* Free software: MIT license
* Documentation: https://django-interlink.readthedocs.io.


Requirements
------------

* Python 2.7 or 3.4+
* Django >= 1.8


Usage
-----

Set some defaults:

    .. code-block:: python
      # settings.py
      INTERLINK_LINKS_PER_PAGE = 8
      INTERLINK_QUERYSETS = 'yourproject.interlink_settings.querysets'

Implement querysets for looking up objects:

    .. code-block:: python
      # interlink_settings.py

      from interlink import QuerySets

      class SiteQuerySets(QuerySets):
          def available_objects(self):
              """
              All the site's donors: the pages on which to place links.
              """
              return [
                  Page.objects.all().order_by('pk'),
              ]

          def relevant_objects(self, model):
              """
              Relevant pages for a given model.
              """
              return [
                  Page.objects.all().order_by('pk'),
              ]


      querysets = SiteQuerySets()

Django admin integration:

    .. code-block:: python

      from interlink.admin import KeywordsInline

      class PageAdmin(admin.ModelAdmin):
        ...
        inlines = [KeywordsInline, ]

More detailed documentation is available on https://django-interlink.readthedocs.io.

Credits
---------

Django-interlink was written by `Alex Morozov`_.

.. _`Alex Morozov`: http://morozov.ca
