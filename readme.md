Runtime Configuration
======================
Create a new OpenShift app:

* `rhc app create -a <app_name> -t diy-0.1`

Login to the application host using the credentials from the above command.  It will look like `ssh://c8812345:123214@<app_name>-namespace.rhcloud.com`:

* `ssh c8812345:123214@<app_name>-namespace.rhcloud.com`

Change into the application tmp directory:

* `cd $OPENSHIFT_TMP_DIR`

Download Python2.7 and extract:

* `wget http://python.org/ftp/python/2.7.3/Python-2.7.3.tar.bz2`
* `tar jxf Python-2.7.3.tar.bz2`

Build and install Python

* `./configure --prefix=$OPENSHIFT_RUNTIME_DIR`
* `make ; make install`

Export new Python path for later configuration (you will need to run this if you logout, etc.):

* `export PATH=$OPENSHIFT_RUNTIME_DIR/bin:$PATH`

Check that new Python is used (should be `Python 2.7.3`):

* `python -V`

Install setuptools and pip

* `cd $OPENSHIFT_TMP_DIR`
* `wget http://pypi.python.org/packages/source/s/setuptools/setuptools-0.6c11.tar.gz`
* `tar zxf setuptools-0.6c11.tar.gz`
* `cd setuptools-0.6c11`
* `python setup.py install`
* `cd $OPENSHIFT_TMP_DIR`
* `wget http://pypi.python.org/packages/source/p/pip/pip-1.1.tar.gz`
* `tar zxf pip-1.1.tar.gz`
* `cd pip-1.1`
* `python setup.py install`


Application Setup
===================

Clone / Fork this repo.

Add an upstream to OpenShift:
* switch into your local repo `cd <app_name>`
* `git remote add upstream -m master git://github.com/openshift/openshift-diy-py27-django.git`
* `git pull -s recursive -X theirs upstream master`
* `git push`

* Note
=======
If you change the Django application name (in the repo it's named `app`) you will also need to update the `.app_name` file with the new name in order for the OpenShift start/stop scripts to work.
