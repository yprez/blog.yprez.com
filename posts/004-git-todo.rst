Searching code for "TODO" comments with git grep
================================================

:date: 2012-10-7 22:00
:tags: git, grep, todo
:category: General

My code, like most code, tends to contain TODO/FIXME comments for things
I don't want to bother with at the time of writing them. Sometimes these
tend to pile up. A quick method of finding those is `git grep`:

.. code-block:: bash

    $ git grep TODO


Today I was looking for "TODO" annotations in an old project,
and completely missed a couple of FIXMEs due to being too lazy to grep for
them. This would have caught them:

.. code-block:: bash

    $ git grep -e TODO -e FIXME


But that's too much typing, so why not make an alias for it?

.. code-block:: cfg

    [alias]
        todo = grep -n -e TODO -e FIXME -e XXX -e OPTIMIZE


And then...

.. code-block:: bash

    $ git todo
    celeryconfig.py:7:        # TODO: find best schedule to avoid query limits
    models.py:38:    # FIXME: remove this method soon


Ok, that was fun, back to work...

**Notes:**

* On a general note - don't let TODOs and FIXMEs pile up in the first 
  place. If it's easy to fix - fix it. If not, document it or open an issue.
