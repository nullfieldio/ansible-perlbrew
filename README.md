Perlbrew
=========

This "perlbrew" role allow you to install perlbrew on Ubuntu / Debian / CentOS | RedHat.

[Perlbrew](http://perlbrew.pl) is a admin-free perl installation management
tool.

Requirements
------------

Ansible 1.9.x

Tested on
---------

2.2.2.0

Role Variables
--------------

* "perl_version" is used to specify the default perl version. Note: This cannot be `latest`, but need to be something like `perl-5.26.1`. The default will be changed to the latest stable.
* "perlbrew_user" is used to specify which user on the remote system that will get perlbrew.
* "switch_to_new_perl" is used to activate (`perlbrew switch`) the new perl_version right away, default is `true` (if `false` added lines in `.profile`/`.bashrc` will be commented)
* "perlbrew_as" name of the perlbrew namespace, default is perl_version

Example config:

    ---
    perl_version: perl-5.26.1
    perlbrew_user: www
    switch_to_new_perl: true
    perlbrew_as: myperl

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
        - role: perlbrew 
          perlbrew_user: tobybro
          perl_version: perl-5.26.1
          perlbrew_as: myawesomeperl

If you are using Ubuntu, you may want to add this to the beginning of your playbook to have it update your Ubuntu before trying to install, this could save you grief:

~~~yaml
---
- hosts: all
  become: yes

  pre_tasks:
  - name: Update cache before we get into anything
    apt:
      state: latest
      force_apt_get: true
      update_cache: true
      cache_valid_time: 3600
    become: yes
    when: ansible_distribution == 'Debian' or ansible_distribution == 'Ubuntu'
~~~

[Vagrant](Vagrant)
-------

For testing the role in a virtual machine a 'Vagrantfile' and 'vagrant-inventory' file is provided (vagrantfiles for short). 
You need Vagrant installed to use it. It is assumed that there is a user vagrant in the vm.

Inside the directory of these two files say:
- 'vagrant up' to set up the virtual machine and run the test, i.e. running the playbook in ./tests/playbook.yml
- 'vagrant destroy' to delete the virtual machine

A CentOS-7.4 is used for the test. Ubuntu is prepared in the vagrantfiles. Adapt it to your needs.


License
-------

BSD

Author Information
------------------

Original author: Jan Henning Thorsen - jhthorsen@cpan.org - http://thorsen.pm
Slightly modified by: Toby Broyles
