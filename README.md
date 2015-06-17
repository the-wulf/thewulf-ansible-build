# thewulf-ansible-build
automated build for the wulf django app

assumes the following technologies::
- ansible (python 2.7 on host machine)
- vagrant
- virtualbox

### getting started
- clone the repo into a directory (preferably called thewulf) -> `git clone https://github.com/the-wulf/thewulf-ansible-build.git ~/Work/thewulf`
- navigate into the directory and run `vagrant up` !! this command _will_ take a while !!
- when the machine has finished provisioning run `vagrant ssh` and your dev environment awaits you

#### misc.
- there are two shared folders between the virtual machine
  - /vagrant/ -> thewulf/  # the directory containing Vagrantfile
  - /home/vagrant/thewulf.org/thewulf -> thewulf/thewulf  # the django project directory
- a pip cache is setup in the vagrant users home dir, if this annoys you -> on the remote machine `rm -rf ~/.pip`
- in order to emulate the dreamhost server, as much of the software as possible is installed into ~/opt
  - while this makes installing software a bit more difficult and slow its still good to setup the vagrant box as closely as possible to the production server.
- when developing on the remote machine attempt to not use sudo as we are not sudoers on dreamhost, nor should we be here.
- some conveniences have been added to the `~/.bash_profile` most notibly the `workon __domain__` function. ex. `workon thewulf.org` will activate the virtualenv and change your directory to the related django project... `deactivate` at anytime to leave the virtualenv.
- the mysql database user is named `thewulf` and doesn't use a password (for sake of simplicity)
- forwarded ports include 80 -> 8080 for apache, 8000 -> 8000 for django dev, 3306 -> 8306 for mysql
- apache is setup with Passenger to serve the django wsgi app. passenger_wsgi.py files simply define the python path and which django settings file to utilize. honesly Passenger and apache are very out of date, but for the sake of emulating the production environment they are setup here.

### todos.
- setup a media server instance on the same dev box with a generic apache file server conf to serve our uploaded assets.
- setup uwsgi + nginx -- the apache passenger stuff is rediculous
- find better mirrors for downloading .tar files
