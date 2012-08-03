Django Bash completion
======================

:tags: django, python, bash
:category: General
:date: 2012-08-26 22:00

A couple of days ago, while browsing the Django repository on Github, I
discovered the `django_bash_completion`_ script (only took me 2 years to
find it). Shortly after the `mind=blown` moment, I tested it and was
amazed by the results, or rather by the fact that I never knew it existed,
although it's referenced in the `docs`_.

Installation was really simple, and outlined in the script itself::

	# Testing it out without installing
	# =================================
	#
	# To test out the completion without "installing" this, just run this file
	# directly, like so:
	#
	#     . ~/path/to/django_bash_completion
	#
	# Note: There's a dot ('.') at the beginning of that command.
	#
	# After you do that, tab completion will immediately be made available in your
	# current Bash shell. But it won't be available next time you log in.
	#
	# Installing
	# ==========
	#
	# To install this, point to this file from your .bash_profile, like so:
	#
	#     . ~/path/to/django_bash_completion
	#
	# Do the same in your .bashrc if .bashrc doesn't invoke .bash_profile.
	#
	# Settings will take effect the next time you log in.

The result:

.. code-block:: bash

	$ python manage.py [TAB]
	cleanup           diffsettings      inspectdb         runfcgi           sqlall
	...

Since I have Django projects deployed on almost every VPS that I access,
I decided to write a small script to install it on a remote machine easily.

.. code-block:: bash

	#!/bin/bash
	# install_django_bash_completion.sh

	DIR=~/scripts

	mkdir $DIR
	wget https://raw.github.com/django/django/master/extras/django_bash_completion -P $DIR
	echo -e "\n\n#Django bash comletion:\nsource $DIR/django_bash_completion" >> ~/.bashrc

And execute it via::

	cat install_django_bash_completion.sh | ssh my.server.com

**Notes:**

* Yes, I know that Zsh auto-completes Django management commands
  (and much more), but I prefer to stick with Bash for now.
* The script is located at ``site-packages/django/extras`` when you install
  Django. But I wanted something more generic as it's located in different
  virtualenvs on every machine.


.. _`django_bash_completion`: https://github.com/django/django/blob/master/extras/django_bash_completion
.. _`docs`: https://docs.djangoproject.com/en/dev/ref/django-admin/#bash-completion