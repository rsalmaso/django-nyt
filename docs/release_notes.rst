Release Notes
=============

1.4.2 (2025-04-23)
------------------

**Added**

* Django 5.2 support #146 (Daniel Grießhaber)


1.4.1 (2024-08-21)
------------------

**Added**

* Django 5.1 support #145 (Benjamin Balder Bach)

1.4 (2024-02-16)
----------------

Hello 👋️ We're alive and maintaining this!

This release puts django-nyt a step forwards toward being a mature framework, especially by adding Django 5 support, fixing issues and adding more tests.
However, there are still some async capabilities remaining to be solved for it to be both mature and modern.

If you can get behind :doc:`the concept </index>`, please consider the great potential of contributing to this project!


**Added**

* Custom email templates per notification type:
  For instance, a site admin and a user may now receive different notification emails, both for content and subject line.
  This is controlled by two new dictionaries in your settings ``NYT_EMAIL_TEMPLATE_NAMES`` and ``NYT_EMAIL_SUBJECT_TEMPLATE_NAMES``.
  Templates are matched to a notification key pattern that uses glob expressions,
  so it's now encouraged to use ``/`` separators in notification keys,
  for instance ``comments/new`` is matched by ``comments/**``. #125 (Benjamin Balder Bach)
* Django 5 support #128 (Benjamin Balder Bach)
* New arguments ``--domain`` and ``--http-only`` for management command ``notifymail``. #130 (Benjamin Balder Bach)
* Documentation reorganized with Diataxis structure and more how-to guides have been added. (Benjamin Balder Bach)
* New shortcut function ``utils.unsubscribe()``. #137 (Benjamin Balder Bach)
* Better logging for ``notifymail`` management command #141 (Benjamin Balder Bach)
* Added fields ``created`` and ``modified`` on models ``Settings`` and ``Subscription`` #142 (Benjamin Balder Bach)

**Changed**

* Tests migrated to pytest #123 (Benjamin Balder Bach)
* Default email notification paths are changed to ``notifications/emails/default.txt`` and ``notifications/emails/default_subject.txt`` #125 (Benjamin Balder Bach)
* Notification URLs added to emails have a hard-coded `https://` (before, this was `http://`) #125 (Benjamin Balder Bach)
* New test-friendly settings pattern changes internal names of settings, but has no effects on Django settings #127 (Benjamin Balder Bach)
* Corrected name of method to ``Settings.get_default_settings`` #129 (Benjamin Balder Bach)
* Improvements to docstrings of main methods ``notify()`` and ``subscribe()`` #129 (Benjamin Balder Bach)
* Return value of ``notify()`` was changed - it no longer returns an `int` (number of created notifications), instead it returns a list of created notifications.
  This is very useful, see :doc:`howto/object_relations` #134 (Benjamin Balder Bach)
* The field ``Notification.url`` now accepts 2,000 characters rather than 200 #142 (Benjamin Balder Bach)

**Fixed**

* Template files possible for email subjects. Previously, this file was ignored #125 (Benjamin Balder Bach)
* Notifications without URLs had a broken URL in emails #125 (Benjamin Balder Bach)
* Management command ``notifymail`` to send emails is more robust #129 (Benjamin Balder Bach)
* ``Settings.save`` recursively called itself when adding a non-default setting #140 (Benjamin Balder Bach)
* Weekly digests weren't correctly generated #142 (Benjamin Balder Bach)

**Removed**

* Python 3.7 support removed #129 (Benjamin Balder Bach)
* Unused (!) setting ``NYT_ENABLED`` was removed #134 (Benjamin Balder Bach)

1.3 (2023-05-03)
----------------

* Hatch build system, environment management and more #116 (Oscar Cortez)
* pre-commit configuration updated #116 (Oscar Cortez)
* Code-base black'ned #116 (Oscar Cortez)


1.2.4 (2022-11-11)
------------------

* Adds Django 4.1 support #113 (Oscar Cortez)


1.2.3
-----

* Add missing .txt email template files in distributed packages #109


1.2.2
-----

* Adds a no-op migration because of auto-detected changes


1.2.1
-----

* Django 4.0 and Python 3.10 support (added to test matrix)


1.2
---

Added
^^^^^

* Django 3.2 and Python 3.9 support (added to test matrix)
* Travis replaced with Circle CI

Removed
^^^^^^^

* Django 1.11 and 2.1 support


1.1.6
-----

Added
^^^^^

* Django 3.1 support (added to test matrix)

1.1.5
-----

Fixed
^^^^^

* Do not access ``Settings.user`` in ``Settings.clean()`` on blank new objects :url-pr:`92`


1.1.4
-----

Added
^^^^^

* Django 3.0 support (added to test matrix)


1.1.3
-----

Added
^^^^^

* Django 2.2 support (added to test matrix)
* Linting (no changes to functionality)


1.1.2
-----

Added
^^^^^

* Django 2.1 support (no changes in code)


1.1.1
-----

Added
^^^^^

* Python 3.7 support  :url-pr:`81`

Deprecations
^^^^^^^^^^^^

* Removed ``django_nyt.notify``, use ``django_nyt.utils.notify``



1.1
---

New features
^^^^^^^^^^^^

* Django 2.0 support :url-pr:`55`

Bug fixes
^^^^^^^^^

* Restored missing translation files :url-pr:`73`

Deprecations
^^^^^^^^^^^^

* Django < 1.11 support is dropped :url-pr:`62`
* Python < 3.4 support is dropped :url-pr:`65` and :url-pr:`68`
* Deprecate ``django_nyt.urls.get_pattern``, use ``include('django_nyt.urls')`` instead :url-pr:`63`
* Removed ``django_nyt.VERSION``, use `django_nyt.__version__` instead :url-pr:`73`

1.0
---

Starting from django-nyt 1.0, support for the upcoming
`channels <https://channels.readthedocs.io/en/stable/>`_ has been added together with
Django 1.9, 1.10 and 1.11 support.

You can switch off django-channels by setting
``settings.NYT_CHANNELS_DISABLE = True``.


New features
^^^^^^^^^^^^

* Support for ``channels`` and web sockets. :url-pr:`21`
* Django 1.9, 1.10, and 1.11 support :url-pr:`25`
* Default AppConfig ``"django_nyt.apps.DjangoNytConfig"`` :url-pr:`57`


Bug fixes
^^^^^^^^^

* Celery will auto-load ``django_nyt.tasks`` when ``channels`` isn't installed :url-issue:`23`
* Error in channels consumer when requested with AnonymousUser (Benjamin Bach) :url-issue:`50` :url-pr:`51`
* Clear the notification type cache every time a new notification type is created or deleted (Benjamin Bach) :url-issue:`34` :url-pr:`36`
* Explicitly accept WebSocket connections (Kim Desrosiers) :url-pr:`35`
* Fix critical django-channels err (Tomaž Žniderič) :url-issue:`29`
* Correctly set default options for ``notifymail`` management command (Benjamin Bach) :url-pr:`32`
* Adds Django 1.11 to test matrix (Benjamin Bach) :url-pr:`32`
* Do not return ``bytes`` in ``__str__`` (Øystein Hiåsen) :url-pr:`28`


Deprecations
^^^^^^^^^^^^

* Django 1.5 and 1.6 support is dropped
