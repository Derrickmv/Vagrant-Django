# Vagrant Set-Up
----
## 1. Set-Up Vagrant
Install Vagrant and VirtualBox

* [https://www.vagrantup.com/downloads.html](https://www.vagrantup.com/downloads.html)
* [https://www.virtualbox.org/](https://www.virtualbox.org/)

Create directory structure required by the Vagrantfile and cd into said working directory

    mkdir directory
    cd directory

Manually copy Vagrantfile and/or any shell scripts into the working directory

Launch vagrant instance

    vagrant up

Once your local virtual machine is running, ssh

    vagrant ssh

Default username is vagrant, group is vagrant (vagrant:vagrant)

## 2. Create virtualenv and pull source code
Set permissions on app directory within /home/vagrant/

    sudo chown vagrant:vagrant /vagrant

Create virtualenv in app directory

    virtualenv miramax_com

Clone app repo into app directory

    cd miramax_com/miramax_com
    git init
    git clone git@bitbucket.org:miramax_com/miramax_com.git

Create your own settings_local file since its in repo's .gitignore

    #Copy the following into your own settings_local.py
    #END

Next, cd into app directory and bin/activate

    source bin/activate

Install pip requirements

    pip install -r requirements.txt

## 3. Configure Apache config
Add localhost as the last line apache2.conf file

    sudo vi /etc/apache2/apache2.conf
    ServerName localhost

Additionally, find line that says User ${APACHE_RUN_USER} and Group ${APACHE_RUN_GROUP} and change both to vagrant

    User vagrant
    Group vagrant

## 4. Configure Django
Create your database

    CREATE DATABASE test_db;
    create user ‘vagrant’@‘localhost’ identified by ‘password’;
    grant all privileges on test_db.* to ‘vagrant’@‘localhost’;
    flush privileges;

Sync your database, migrate, collecstatic

    python manage.py syncdb
    python manage.py migrate
    python manage.py collectstatic


----

#### changelog
* April-2016
