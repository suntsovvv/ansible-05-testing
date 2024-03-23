Lighthouse-role
=========

Deploy lighthouse using ansible

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------
|vars|description|
|---------|----------------|
| lighthouse_vcs | url lighthouse reposytory for install |
| lighthouse_local_dir | directory of lighthouse files for nginx |
| nginx_user_name | username with whose rights Nginx starts |
| lighthouse_port | port of lighthouse servise |

ighthouse_por
Dependencies
------------
Nginx

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: lighthouse-role }

License
-------

MIT

Author Information
------------------

Vadim Suntsov
