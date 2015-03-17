========================
Plone Conf 2015 buildout
========================

.. contents ::

Prerequisitements
-----------------

================  ===================  ===============
Debian/Ubuntu     CentOS               dependency for 
================  ===================  ===============
python 2.7        python 2.7           buildout
python-dev        python-devel         buildout
python-test       python-test          buildout
wget              wget                 buildout
gcc               gcc                  buildout
libxml2-dev       libxml2-devel        buildout
libxslt-dev       libxslt-devel        buildout
libjpeg-dev       libjpeg-turbo-devel  Pillow
automake          automake             varnish
autotools-dev     autoconf             varnish
libedit-dev       libedit-devel        varnish
libjemalloc-dev   jemalloc-devel       varnish
libncurses-dev    ncurses-devel        varnish
libpcre3-dev      pcre-devel           varnish
libtool           libtool              varnish
pkg-config        pkgconfig            varnish
python-docutils   python-docutils      varnish
python-sphinx     python-sphinx        varnish
================  ===================  ===============

Connect
-------

Connect to the production server (10.0.0.56) using your local account.

Deploy
------
::

  $ su zope-www
  $ cd /var/local/ploneconf2015.buildout
  $ git pull
  $ ./install.sh
  $ bin/buildout

First run
---------
::

  $ bin/varnish
  $ bin/zope-start

Restart
-------
::

  $ bin/zope-restart

Stop
----
::

  $ kill -9 `cat parts/varnish/varnish.pid`
  $ bin/zope-stop
  
Update
------
::

  $ su zope-www
  $ cd /var/local/ploneconf2015.buildout
  $ git pull
  $ bin/develop up
  $ bin/buildout
  $ bin/zope-restart
  $ parts/varnish-build/bin/varnishadm
  > stop
  > start

Cron jobs
----------
::

  $ crontab -u zope-www -e
  @reboot cd /var/local/ploneconf2015.buildout && bin/varnish && bin/zope-start
