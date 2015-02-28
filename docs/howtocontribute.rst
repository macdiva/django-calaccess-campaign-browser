How to contribute
=================

This walkthrough will show you how to install the source code of this application
to fix bugs and develop new features. Use `Python 2.7 <https://www.python.org/downloads/>`_.

First create a new virtualenv.

.. code-block:: bash

    $ virtualenv django-calaccess-campaign-browser

Jump in.

.. code-block:: bash

    $ cd django-calaccess-campaign-browser
    $ . bin/activate

Clone the repository from `GitHub <https://github.com/california-civic-data-coalition/django-calaccess-campaign-browser>`_.

.. code-block:: bash

    $ git clone https://github.com/california-civic-data-coalition/django-calaccess-campaign-browser.git repo

Move into it and install the Python dependencies.

.. code-block:: bash

    $ cd repo
    $ pip install -r requirements_dev.txt

Make sure you have MySQL installed. If you don't, now is the time to hit Google and figure out how. If
you're using Apple's OSX operating system, you can `install via Homebrew <http://thisdotlife.com/2013/05/30/how-to-install-mysql-on-mac-os-x-using-homebrew-tutorial/>`_. If you need to clean up after a previous MySQL installation, `this might help <http://stackoverflow.com/questions/4359131/brew-install-mysql-on-mac-os/6378429#6378429>`_.

Then create a new database named ``calaccess``.

.. code-block:: bash

    mysqladmin -h localhost -u root -p create calaccess

If you have a different username, substitute it above. You'll be prompted for that user's mysql password.

Then create a file at ``example/project/settings_local.py`` to save your custom database credentials. That
might look something like this.

.. code-block:: python

    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.mysql',
            'NAME': 'calaccess',
            'USER': 'yourusername',
            'PASSWORD': 'yourpassword',
            'HOST': 'localhost',
            'PORT': '3306',
            'OPTIONS': {
                'local_infile': 1,
            }
        }
    }

Finally create your database and get to work.

.. code-block:: bash

    $ python example/manage.py migrate

You might start by loading the data dump from the web.

.. code-block:: bash

    $ python example/manage.py downloadcalaccessrawdata

Then you can build the campaign finance models

.. code-block:: bash

    $ python example/manage.py buildcalaccesscampaignbrowser

And fire up the Django test server to use the browser

.. code-block:: bash

    $ python example/manage.py collectstatic
    $ python example/manage.py runserver
