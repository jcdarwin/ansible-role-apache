ansible-role-apache
===================

An Ansible role, available via [Ansible Galaxy](https://galaxy.ansible.com), that installs and configures apache on Ubuntu.

This role works with [our repo to create a vagrant virtualbox vm](https://github.com/jcdarwin/ansible-roles-vagrant), but is easily modifed to work with actual ubuntu boxes.

You'll probably want to amend / override:

* `defaults/main.yml`

Installation
------------

Preusming a `requirements.yml` as follows:

    # Install a role from GitHub
    - name: ansible-role-apache
    src: https://github.com/jcdarwin/ansible-role-apache

We can install the role locally, using a `requirements.yml` file:

    # Install a role from GitHub
    - name: ansible-role-apache
    src: https://github.com/jcdarwin/ansible-role-apache
    path: roles/

Install the role:

    ansible-galaxy install -r requirements.yml -p ./roles


Requirements
------------

You may already have:

* Created a vagrant VirtualBox virtual machine using [ansible-roles-vagrant](https://github.com/jcdarwin/ansible-role-users)
* Provisioned the virtual machine with users using [ansible-role-users](https://github.com/jcdarwin/ansible-role-users)
* Installled various common packages using [ansible_role_common](https://github.com/jcdarwin/ansible-role-common)
* Installed and configured MySQL using [ansible_role_mysql](https://github.com/jcdarwin/ansible-role-mysql)
* Installed and configured PHP using [ansible_role_php](https://github.com/jcdarwin/ansible-role-php)

Role Variables
--------------

Available variables are listed below, along with default values as found in `defaults/main.yml`:

    ansible_role_php:
      packages:
      - php5
      - php5-curl
      - php5-mcrypt
      - php5-gd
      - php5-mysql
      - php5-cli
      - php5-imagick

Dependencies
------------

None.

Example Playbook
----------------

Our `hosts` file, as generated by [our repo to create a vagrant virtualbox vm](https://github.com/jcdarwin/ansible-roles-vagrant):

    [vagrant]
    host1 ansible_ssh_host=127.0.0.1 ansible_ssh_port=2222 ansible_user=vagrant ansible_ssh_private_key_file=../.vagrant/machines/default/virtualbox/private_key

We include a playbook at `main.yml`.

Running the playbook:

    # Note that we're presuming our hosts file has been generated by our vagrant repo
    ansible all -m ping -i ../vagrant/ansible/hosts -l all

    ansible-playbook -l all main.yml -i ../vagrant/ansible/hosts

    # Check that php has been installed
    ansible -m shell -a 'php -v' all -i ../vagrant/ansible/hosts

To see the something in the browser (presuming you're using the defaults and have installed the `ansible-role-php` role):

	# Add the subdomain to our hosts file
	echo "127.0.0.1	localhost.vagrant"

	# then visit: http://localhost.vagrant/info.php

License
-------

MIT

Author Information
------------------

http://github.com/jcdarwin
