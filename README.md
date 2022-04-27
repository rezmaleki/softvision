# softvision
PyPI Server
===========

[![](https://images.microbadger.com/badges/image/codekoala/pypi.svg)](https://microbadger.com/images/codekoala/pypi "Get your own image badge on microbadger.com")

This is a ansible playbook which runs a simple PyPI server that can be used to host internal packages and
versions of packages that are suitable for use with proprietary products.

.htpasswd via ansible vault 
--------------------
.htpasswd file will go through the ansible vault
default .htpasswd
the password is 'soft*******123'

to encrypt your own .htpasswd file use
ansible-vault encrypt .htpasswd

Ansible 
===========
This part consists of a host inventory and 2 playbooks. 

hosts
-------
Inside the “hosts” file, change the IP address in “target” group to the IP address of the
target server and make sure there is no connection restriction from the workstation to the Instance
Inside the inventory file, IP address of the destination server should be provided. For Ansible to connect to target server, required
information such as the username to connect or the SSH key to use.

deploy.yml
-----------
The deploy.yml playbook consists of several task which first, update the operation system and
then install the required packages such as docker-ce and pip .
Then it would create required files and directory. At the end it will pull the images  and bring up the container.


Once running, you should be able to visit http://localhost:8080 to see the
landing page for your very own PyPI server.

You can add Python packages to the server simply 

test.yml
-----------




environment variable PYPI_AUTHENTICATE
----------------------------------------
 list of (case-insensitive) actions to authenticate. Default to update
 but we set it to update,download,list while running the container

Adding Internal Packages
------------------------

Internal packages may be uploaded to this PyPI server quite easily. The first
step is to create a user account:

    htpasswd -s /srv/pypi/.htpasswd yourusername

Adding Third Party Packages
---------------------------

Third party packages can be mirrored on the PyPI server by using a command such
as:

    pip install -d /srv/pypi pkgname


HOW TO RUN
----------------

    ansible-playbook --ask-vault-pass -i hosts deploy.yml 

