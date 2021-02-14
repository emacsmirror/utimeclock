##########
uTimeClock
##########

Simple manual time tracking.

This is a time tracking utility, intended to be used in any text mode such as reStructuredText, MarkDown and ORG.

Instead of defining a mode, this package simply provides functions to:

- Clock on/off.
- Report accumulated time.

Available via `melpa <https://melpa.org/#/utimeclock>`__.


Motivation
==========

Automatic time tracking packages tend to assume you're editing a buffer with the primary purpose of tracking time.

This package uses a terse time tracking format which can easily be maintained along side other notes.


Usage
=====

This package exposes the following functions:


- ``utimeclock-show-summary`` Reports accumulated time.
- ``utimeclock-toggle`` Clock on/off using the time declaration, automatically pairing up time-ranges.
- ``utimeclock-insert`` Simply insert the current time, without the more advanced functionality toggle provides.


Examples
--------

This is a typical example of time being logged.

::

   time: 08:20-09:20 01:30-02:55 03:02-05:20 05:40-06:25 06:50-07:50

In cases when time segments don't fit well on a single line,
they are automatically split before ``fill-column`` (see ``utimeclock-split-at-fill-column``).

Longer example using seconds, split onto multiple lines.

::

   time: 8:50:17-9:50:55 10:40:01-12:10:13 3:20:22-6:05:03 \
         6:15:19-6:30:48 6:35:51-06:45:38 7:00:12-07:34:09 \
         8:30:05-9:15:29 9:30:44-12:00:00


Details
-------

While this is a simple package it's worth mentioning some the details of how it works.

- Clock on/off shows a message of the time spent away/working.
- When there is a selection ``utimeclock-show-summary`` shows only times within the selection.
- When showing a summary the last time is detected by searching backwards
  for ``utimeclock-time-prefix`` from the end of the current line.
- Extra spaces between times are ignored.


Customization
-------------

Note that these can be left as default for typical usage.

``utimeclock-time-prefix`` (``time:``)
   The text used to identify the beginning of a series of time ranges.
``utimeclock-time-pair`` (``-``)
   Text separating time ranges.

   By default time ranges use a dash, for example: ``1:30-2:30 3:00-3:30``.

``utimeclock-split-at-fill-column`` (``t``)
   When true, adding times that exceed the ``fill-column`` will be wrapped onto the next line.

``utimeclock-line-separator`` (``\``)
   Text used at the end of lines to allow a series of time-ranges to be written across multiple lines.
``utimeclock-12-hour-clock`` (``nil``)
   Use a 12 hour clock when logging times.
``utimeclock-time-precision`` (``minutes``)
   The precision to report time in, can be (``hours``, ``minutes``, ``seconds``).


Limitations
===========

Unsupported features:

- Daylight savings.
- Time spans longer than 24 hours.


Installation
============

The package is `available in melpa <https://melpa.org/#/utimeclock>`__ as ``utimeclock``.

.. code-block:: elisp

   (use-package utimeclock)

An example using key bindings:

.. code-block:: elisp

   (use-package utimeclock
     :config
     (global-set-key (kbd "<f5>") 'utimeclock-toggle)
     (global-set-key (kbd "<f6>") 'utimeclock-show-summary))


Alternatives
============

See `track time <https://melpa.org/#/?q=track%20time>`__ search in Melpa for alternatives.

At the time of writing most of them are much more sophisticated than this package, with features such as:

- Automatically detecting activity.
- Storing time data in external files.
- Integrating with org-mode adjenda.

While these may be useful, the intention for this package is to be minimal,
allowing you to track time without needing to buy into a more complex system.
