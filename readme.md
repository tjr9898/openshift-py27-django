Runtime Configuration
======================
Create a new OpenShift app:

* `rhc app create -a <app_name> -t diy-0.1`

Application Setup
===================

Clone / Fork this repo.

Add an upstream to OpenShift:
* switch into your local repo `cd <app_name>`
* `git remote add upstream -m master git@github.com:tjr9898/openshift-py27-django.git`
* `git pull -s recursive -X theirs upstream master`
* `git push`

* Note
=======
If you change the Django application name (in the repo it's named `app`) you will also need to update the `.app_name` file with the new name in order for the OpenShift start/stop scripts to work.
