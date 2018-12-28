[![Build Status](https://travis-ci.org/nickmaccarthy/ansible-role-logstash.svg?branch=master)](https://travis-ci.org/nickmaccarthy/ansible-role-logstash.svg?branch=master)

Ansible Role: Logstash
=========

A quick and easy role to install logstash. 

Note: configuration of logstash (filters, inputs, outputs, etc) should come from a different role.  

Inspired by [geerlingguy.logstash](https://github.com/geerlingguy/ansible-role-logstash)

Requirements
------------

```
java 1.8+ ( try the ansible role geerlingguy.java -- openjdk works fine too )
```

Role Variables
--------------
```
logstash_version: '6.x'
```
Which Logstash version would like to install 

```
logstash_dir: /usr/share/logstash
```
The directory where we install logstash 

```
logstash_ssl_dir: /etc/pki/logstash
logstash_ssl_certificate_file: ""
logstash_ssl_key_file: ""
```
From the `geerlingguy.logstash` role:  Local paths to the SSL certificate and key files, which will be copied into the `logstash_ssl_dir`.

For utmost security, you should use your own valid certificate and keyfile, and update the `logstash_ssl_*` variables in your playbook to use your certificate.

To generate a self-signed certificate/key pair, you can use use the command:

    $ sudo openssl req -x509 -batch -nodes -days 3650 -newkey rsa:2048 -keyout logstash.key -out logstash.crt

Note that filebeat and logstash may not work correctly with self-signed certificates unless 

```
logstash_enabled_on_boot: true
```
Wether or not we should start logstash when the system boots up 

```
logstash_install_plugins:
  - logstash-input-beats
```
A list of logstash plugins to install 


Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```
    - hosts: servers
      roles:
         - role: geerlingguy.elasticsearch
         - role: nickmaccarthy.logstash
```

Role for more than one logstash instance on the same host
```
  - hosts: servers
    roles:
      - role: nickmaccarthy.logtstash
        vars:
          logstash_dir: /usr/share/logstash-beats-receiver 

      - role: nickmaccarthy.logstash
        vars:
          logstash_dir: /usr/share/logstash-shipper 
```
License
-------

MIT/BSD

Author Information
------------------

Created by [Nick MacCarthy](http://nickmaccarthy.com) in 2018 
