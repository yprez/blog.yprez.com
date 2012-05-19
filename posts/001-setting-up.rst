Setting Up
==========

:date: 2012-05-19 18:00
:tags: python, pelican
:category: General

I decided to set up this blog mainly as an experiment.

I might write might write some Python and software dev related posts sometime
soon.

This blog is powered by `Pelican`_, the posts are written in
reStructuredText and it's hosted on `Github Pages`_.

I'm keeping the `source repository`_ separate from the `generated files`_
repository. Committing to the second when it's ready to update.

Setting up:

.. code-block:: bash

    git submodule add git@github.com:yprez/yprez.github.com.git output
    pelican . --output=output --settings=settings.py

    cd output
    git add .
    git commit -am"Set up blog"
    git push

.. _`Pelican`: http://alexis.notmyidea.org/pelican/
.. _`Github Pages`: http://pages.github.com/
.. _`source repository`: https://github.com/yprez/blog.yprez.com
.. _`generated files`: https://github.com/yprez/yprez.github.com

