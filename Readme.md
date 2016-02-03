# Heroku buildpack: Python

## DEPRECATED

The [official heroku python buildpack](https://github.com/heroku/heroku-buildpack-python) has pip 8 included by default. [You should use it an the new requirements file with hashes format](https://github.com/erikrose/peep/wiki/UpgradeToPip8).

![python-banner](https://cloud.githubusercontent.com/assets/51578/8914205/ecf2047c-346b-11e5-98c5-42547f9f4410.jpg)

This is a fork of the [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for Python apps, powered by [pip](http://www.pip-installer.org/) and [peep](https://github.com/erikrose/peep).


Usage
-----

The only additional thing you need to do to use this over the official Heroku Python buildpack is to add the hashes to your requirements file(s) so that peep will successfully complete the install. If you don't do this peep will fail and give a good explanation as to why.

Example usage:

    $ ls
    Procfile  requirements.txt  web.py

    $ heroku create --buildpack git://github.com/pmclanahan/heroku-buildpack-python-peep.git

    $ git push heroku master
    ...
    -----> Python app detected
    -----> Installing runtime (python-2.7.10)
    -----> Installing dependencies using peep
           Downloading requests==2.7.0 (470K)...
           Processing /tmp/peep-PWtR4d/requests-2.7.0-py2.py3-none-any.whl
           Installing collected packages: requests
           Successfully installed requests-2.7.0
           Cleaning up...
    -----> Discovering process types
           Procfile declares types -> (none)

You can also add it to upcoming builds of an existing application:

    $ heroku buildpacks:set git://github.com/pmclanahan/heroku-buildpack-python-peep.git

The buildpack will detect your app as Python if it has the file `requirements.txt` in the root.

It will use Peep to install your dependencies, vendoring a copy of the Python runtime into your slug.

Specify a Runtime
-----------------

You can also provide arbitrary releases Python with a `runtime.txt` file.

    $ cat runtime.txt
    python-3.5.0

Runtime options include:

- python-2.7.10
- python-3.5.0
- pypy-2.6.1 (unsupported, experimental)
- pypy3-2.4.0 (unsupported, experimental)

Other [unsupported runtimes](https://github.com/heroku/heroku-buildpack-python/tree/master/builds/runtimes) are available as well.
