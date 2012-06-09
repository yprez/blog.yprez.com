Running a Bottle app with Gunicorn
==================================

:tags: python, bottle, gunicorn
:category: General
:date: 2012-06-09 19:00

Recently we wrote a simple web tracker at work. Using the `Bottle`_
microframework.

Looking back, maybe I should've used `Flask`_ instead, as I simply don't see
the reason for stuffing 3,000 lines of code in one file, other than a proof of
concept. But both frameworks are quite similar, and both have quite good
documentation.

A simple bottle app looks like this:

.. code-block:: python

    from bottle import route, run

    @route('/')
    def index():
        return '<h1>Hello Bottle!</h1>'

    run(host='localhost', port=8080)

To switch the server to `Gunicorn`_ replace the last line with:

.. code-block:: python

    run(host='localhost', port=8080, server='gunicorn', workers=4)

But want if we want to run it using the ``gunicorn`` executable (to run it with
an ``init.d`` script)? Here things became more problematic.

I assumed it would be as simple as simple as running `gunicorn myapp`, but it
was still running the app with the default server.

It also turns out that Bottle is completely not Googlable, and searching for
``"bottle python gunicorn"`` just returned random crap. After about half an
hour of digging, the solution turned out to be quite simple... I was missing a
WSGI "app" object.

The finished app looks like this:

.. code-block:: python

    import bottle
    from bottle import route, run

    @route('/')
    def index():
        return '<h1>Hello Bottle!</h1>'

    def run_test_server():
        run(host='localhost', port=8080)

    if __name__ == "__main__":
        run_test_server()

    app = bottle.default_app()

The last line sets the "app" object for the WSGI server to run.

Running the test server::

    python hello_bottle.py

Running the app with Gunicorn (with 4 workers)::

     gunicorn -w 4 hello_bottle:app

Simple enough, but it's still a little annoying that this wasn't available in
the documentation.

For comparison, in Flask, a hello world app looks like this:

.. code-block:: python

    from flask import Flask
    app = Flask(__name__)

    @app.route("/")
    def hello():
        return "Hello World!"

    if __name__ == "__main__":
        app.run()

The "app" object is available right away, so we don't have to guess. And the
first result in Google for ``"flask gunicorn"`` is a link to the
`official documentation`_, describing how to run it with various WSGI servers.

In conclusion: Bottle was fun, the application was very easy to build, and runs
incredibly fast. I think that for the next project that requires a
microframework I will use Flask instead. Even if just for the sake of
comparison.

.. _`Bottle`: http://bottlepy.org/
.. _`Flask`: http://flask.pocoo.org/
.. _`Gunicorn`: http://gunicorn.org/
.. _`official documentation`: http://flask.pocoo.org/docs/deploying/others/
