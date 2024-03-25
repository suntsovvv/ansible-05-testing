# Домашнее задание к занятию 5 «Тестирование roles»
## 1   
```bash
user@study:~/home_work/ansible/ansible-04-role/playbook/roles/clickhouse$ molecule test -s centos_7
WARNING  Driver docker does not provide a schema.
CRITICAL Failed to validate /home/user/home_work/ansible/ansible-04-role/playbook/roles/clickhouse/molecule/centos_7/molecule.yml
```
## 2   
```bash
user@study:~/home_work/ansible/ansible-05-testing/roles/vector-role$ molecule init scenario --driver-name docker
INFO     Initializing new scenario default...

PLAY [Create a new molecule scenario] ******************************************

TASK [Check if destination folder exists] **************************************
changed: [localhost]

TASK [Check if destination folder is empty] ************************************
ok: [localhost]

TASK [Fail if destination folder is not empty] *********************************
skipping: [localhost]

TASK [Expand templates] ********************************************************
changed: [localhost] => (item=molecule/default/converge.yml)
skipping: [localhost] => (item=molecule/default/destroy.yml) 
skipping: [localhost] => (item=molecule/default/create.yml) 
changed: [localhost] => (item=molecule/default/molecule.yml)

PLAY RECAP *********************************************************************
localhost                  : ok=3    changed=2    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0

INFO     Initialized scenario in /home/user/home_work/ansible/ansible-05-testing/roles/vector-role/molecule/default successfully.
user@study:~/home_work/ansible/ansible-05-testing/roles/vector-role$
```
## 3   
Добавил в проверку oraclelinux:8 и ubuntu:latest
molecule.yml:   
```yml
---
driver:
  name: docker
lint: |
  ansible-lint .
  yamllint .
platforms:
  - name: centos7
    image: docker.io/pycontribs/centos:7
    pre_build_image: true
  - name: ubuntu
    image: docker.io/pycontribs/ubuntu:latest
    pre_build_image: true
  - name: oraclelinux
    image: docker.io/oraclelinux:8
    pre_build_image: true    
provisioner:
  name: ansible
verifier:
  name: ansible
role_name_check: 1
```
```bash
user@study:~/home_work/ansible/ansible-05-testing/code/vector-role$ molecule test --destroy=never
WARNING  Driver docker does not provide a schema.
INFO     default scenario test matrix: dependency, cleanup, destroy, syntax, create, prepare, converge, idempotence, side_effect, verify, cleanup, destroy
INFO     Performing prerun with role_name_check=1...
WARNING  Computed fully qualified role name of vector-role does not follow current galaxy requirements.
Please edit meta/main.yml and assure we can correctly determine full role name:

galaxy_info:
role_name: my_name  # if absent directory name hosting role is used instead
namespace: my_galaxy_namespace  # if absent, author is used instead

Namespace: https://galaxy.ansible.com/docs/contributing/namespaces.html#galaxy-namespace-limitations
Role: https://galaxy.ansible.com/docs/contributing/creating_role.html#role-names

As an alternative, you can add 'role-name' to either skip_list or warn_list.

INFO     Running default > dependency
WARNING  Skipping, missing the requirements file.
WARNING  Skipping, missing the requirements file.
INFO     Running default > cleanup
WARNING  Skipping, cleanup playbook not configured.
INFO     Running default > destroy
WARNING  Skipping, '--destroy=never' requested.
INFO     Running default > syntax
INFO     Sanity checks: 'docker'

playbook: /home/user/home_work/ansible/ansible-05-testing/code/vector-role/molecule/default/converge.yml
INFO     Running default > create
WARNING  Skipping, instances already created.
INFO     Running default > prepare
WARNING  Skipping, prepare playbook not configured.
INFO     Running default > converge

PLAY [Converge] ****************************************************************

TASK [Gathering Facts] *********************************************************
ok: [ubuntu]
ok: [oraclelinux]
ok: [centos7]

TASK [Include dir vector role] *************************************************

TASK [vector-role : Get vector distrib] ****************************************
skipping: [oraclelinux]
skipping: [ubuntu]
ok: [centos7]

TASK [vector-role : Install vector packages] ***********************************
skipping: [oraclelinux]
skipping: [ubuntu]
ok: [centos7]

TASK [vector-role : Get vector distrib] ****************************************
skipping: [centos7]
skipping: [oraclelinux]
ok: [ubuntu]

TASK [vector-role : Install vector packages] ***********************************
skipping: [centos7]
skipping: [oraclelinux]
ok: [ubuntu]

TASK [vector-role : Get vector distrib] ****************************************
skipping: [centos7]
skipping: [ubuntu]
ok: [oraclelinux]

TASK [vector-role : Install vector packages] ***********************************
skipping: [centos7]
skipping: [ubuntu]
ok: [oraclelinux]

TASK [vector-role : Generate vector config] ************************************
ok: [centos7]
ok: [ubuntu]
ok: [oraclelinux]

PLAY RECAP *********************************************************************
centos7                    : ok=4    changed=0    unreachable=0    failed=0    skipped=4    rescued=0    ignored=0
oraclelinux                : ok=4    changed=0    unreachable=0    failed=0    skipped=4    rescued=0    ignored=0
ubuntu                     : ok=4    changed=0    unreachable=0    failed=0    skipped=4    rescued=0    ignored=0

INFO     Running default > idempotence

PLAY [Converge] ****************************************************************

TASK [Gathering Facts] *********************************************************
ok: [ubuntu]
ok: [oraclelinux]
ok: [centos7]

TASK [Include dir vector role] *************************************************

TASK [vector-role : Get vector distrib] ****************************************
skipping: [oraclelinux]
skipping: [ubuntu]
ok: [centos7]

TASK [vector-role : Install vector packages] ***********************************
skipping: [oraclelinux]
skipping: [ubuntu]
ok: [centos7]

TASK [vector-role : Get vector distrib] ****************************************
skipping: [centos7]
skipping: [oraclelinux]
ok: [ubuntu]

TASK [vector-role : Install vector packages] ***********************************
skipping: [centos7]
skipping: [oraclelinux]
ok: [ubuntu]

TASK [vector-role : Get vector distrib] ****************************************
skipping: [centos7]
skipping: [ubuntu]
ok: [oraclelinux]

TASK [vector-role : Install vector packages] ***********************************
skipping: [centos7]
skipping: [ubuntu]
ok: [oraclelinux]

TASK [vector-role : Generate vector config] ************************************
ok: [centos7]
ok: [oraclelinux]
ok: [ubuntu]

PLAY RECAP *********************************************************************
centos7                    : ok=4    changed=0    unreachable=0    failed=0    skipped=4    rescued=0    ignored=0
oraclelinux                : ok=4    changed=0    unreachable=0    failed=0    skipped=4    rescued=0    ignored=0
ubuntu                     : ok=4    changed=0    unreachable=0    failed=0    skipped=4    rescued=0    ignored=0

INFO     Idempotence completed successfully.
INFO     Running default > side_effect
WARNING  Skipping, side effect playbook not configured.
INFO     Running default > verify
INFO     Running Ansible Verifier
```
## 4-5

```bash

PLAY RECAP *********************************************************************
centos7                    : ok=4    changed=0    unreachable=0    failed=0    skipped=4    rescued=0    ignored=0
oraclelinux                : ok=4    changed=0    unreachable=0    failed=0    skipped=4    rescued=0    ignored=0
ubuntu                     : ok=4    changed=0    unreachable=0    failed=0    skipped=4    rescued=0    ignored=0

INFO     Idempotence completed successfully.
INFO     Running default > side_effect
WARNING  Skipping, side effect playbook not configured.
INFO     Running default > verify
INFO     Running Ansible Verifier

PLAY [Verify] ******************************************************************

TASK [Get Vector version] ******************************************************
changed: [ubuntu]
changed: [oraclelinux]
changed: [centos7]

TASK [Read Vector config file] *************************************************
ok: [centos7]
ok: [ubuntu]
ok: [oraclelinux]

TASK [Check Version] ***********************************************************
ok: [centos7] => {
    "changed": false,
    "msg": "its all ok"
}
ok: [oraclelinux] => {
    "changed": false,
    "msg": "its all ok"
}
ok: [ubuntu] => {
    "changed": false,
    "msg": "its all ok"
}

TASK [Check nginxdb in vector.yaml] ********************************************
ok: [centos7] => {
    "changed": false,
    "msg": "its all ok"
}
ok: [ubuntu] => {
    "changed": false,
    "msg": "its all ok"
}
ok: [oraclelinux] => {
    "changed": false,
    "msg": "its all ok"
}

PLAY RECAP *********************************************************************
centos7                    : ok=4    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
oraclelinux                : ok=4    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ubuntu                     : ok=4    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

INFO     Verifier completed successfully.
INFO     Running default > cleanup
WARNING  Skipping, cleanup playbook not configured.
INFO     Running default > destroy
WARNING  Skipping, '--destroy=never' requested.
```
### 6   
https://github.com/suntsovvv/vector-role/releases/tag/v1.1.0

## Tox
### 1-6

```bash
 user@study:~/home_work/ansible/ansible-05-testing/code/vector-role$ docker run --privileged=True -v ~/home_work/ansible/ansible-05-testing/code/vector-role:/opt/vector-role -w /opt/vector-role -it aragast/netology:latest /bin/bash
[root@2279a6f2057d vector-role]# tox
py37-ansible212 recreate: /opt/vector-role/.tox/py37-ansible212
py37-ansible212 installdeps: -rtox-requirements.txt, ansible<3.0
py37-ansible212 installed: ansible==2.10.7,ansible-base==2.10.17,ansible-compat==1.0.0,ansible-lint==5.1.3,arrow==1.2.3,bcrypt==4.1.2,binaryornot==0.4.4,bracex==2.3.post1,cached-property==1.5.2,Cerberus==1.3.5,certifi==2024.2.2,cffi==1.15.1,chardet==5.2.0,charset-normalizer==3.3.2,click==8.1.7,click-help-colors==0.9.4,cookiecutter==2.6.0,cryptography==42.0.5,distro==1.9.0,enrich==1.2.7,idna==3.6,importlib-metadata==6.7.0,Jinja2==3.1.3,jmespath==1.0.1,lxml==5.1.0,markdown-it-py==2.2.0,MarkupSafe==2.1.5,mdurl==0.1.2,molecule==3.5.2,molecule-podman==1.1.0,packaging==24.0,paramiko==2.12.0,pathspec==0.11.2,pluggy==1.2.0,pycparser==2.21,Pygments==2.17.2,PyNaCl==1.5.0,python-dateutil==2.9.0.post0,python-slugify==8.0.4,PyYAML==5.4.1,requests==2.31.0,rich==13.7.1,ruamel.yaml==0.18.6,ruamel.yaml.clib==0.2.8,selinux==0.2.1,six==1.16.0,subprocess-tee==0.3.5,tenacity==8.2.3,text-unidecode==1.3,typing_extensions==4.7.1,urllib3==2.0.7,wcmatch==8.4.1,yamllint==1.26.3,zipp==3.15.0
py37-ansible212 run-test-pre: PYTHONHASHSEED='557455390'
py37-ansible212 run-test: commands[0] | molecule test -s tox --destroy always
INFO     tox scenario test matrix: destroy, create, converge, destroy
INFO     Performing prerun...
INFO     Set ANSIBLE_LIBRARY=/root/.cache/ansible-compat/b984a4/modules:/root/.ansible/plugins/modules:/usr/share/ansible/plugins/modules
INFO     Set ANSIBLE_COLLECTIONS_PATH=/root/.cache/ansible-compat/b984a4/collections:/root/.ansible/collections:/usr/share/ansible/collections
INFO     Set ANSIBLE_ROLES_PATH=/root/.cache/ansible-compat/b984a4/roles:/root/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles
INFO     Running tox > destroy
INFO     Sanity checks: 'podman'

PLAY [Destroy] *****************************************************************

TASK [Destroy molecule instance(s)] ********************************************
changed: [localhost] => (item={'image': 'quay.io/centos/centos:stream8', 'name': 'instance', 'pre_build_image': True})

TASK [Wait for instance(s) deletion to complete] *******************************
FAILED - RETRYING: Wait for instance(s) deletion to complete (300 retries left).
changed: [localhost] => (item={'started': 1, 'finished': 0, 'ansible_job_id': '240351440457.148', 'results_file': '/root/.ansible_async/240351440457.148', 'changed': True, 'failed': False, 'item': {'image': 'quay.io/centos/centos:stream8', 'name': 'instance', 'pre_build_image': True}, 'ansible_loop_var': 'item'})

PLAY RECAP *********************************************************************
localhost                  : ok=2    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

INFO     Running tox > create

PLAY [Create] ******************************************************************

TASK [get podman executable path] **********************************************
ok: [localhost]

TASK [save path to executable as fact] *****************************************
ok: [localhost]

TASK [Log into a container registry] *******************************************
skipping: [localhost] => (item="instance registry username: None specified") 

TASK [Check presence of custom Dockerfiles] ************************************
ok: [localhost] => (item=Dockerfile: None specified)

TASK [Create Dockerfiles from image names] *************************************
skipping: [localhost] => (item="Dockerfile: None specified; Image: quay.io/centos/centos:stream8") 

TASK [Discover local Podman images] ********************************************
ok: [localhost] => (item=instance)

TASK [Build an Ansible compatible image] ***************************************
skipping: [localhost] => (item=quay.io/centos/centos:stream8) 

TASK [Determine the CMD directives] ********************************************
ok: [localhost] => (item="instance command: None specified")

TASK [Remove possible pre-existing containers] *********************************
changed: [localhost]

TASK [Discover local podman networks] ******************************************
skipping: [localhost] => (item=instance: None specified) 

TASK [Create podman network dedicated to this scenario] ************************
skipping: [localhost]

TASK [Create molecule instance(s)] *********************************************
changed: [localhost] => (item=instance)

TASK [Wait for instance(s) creation to complete] *******************************
FAILED - RETRYING: Wait for instance(s) creation to complete (300 retries left).
FAILED - RETRYING: Wait for instance(s) creation to complete (299 retries left).
FAILED - RETRYING: Wait for instance(s) creation to complete (298 retries left).
FAILED - RETRYING: Wait for instance(s) creation to complete (297 retries left).
FAILED - RETRYING: Wait for instance(s) creation to complete (296 retries left).
FAILED - RETRYING: Wait for instance(s) creation to complete (295 retries left).
FAILED - RETRYING: Wait for instance(s) creation to complete (294 retries left).
FAILED - RETRYING: Wait for instance(s) creation to complete (293 retries left).
FAILED - RETRYING: Wait for instance(s) creation to complete (292 retries left).
FAILED - RETRYING: Wait for instance(s) creation to complete (291 retries left).
changed: [localhost] => (item=instance)

PLAY RECAP *********************************************************************
localhost                  : ok=8    changed=3    unreachable=0    failed=0    skipped=5    rescued=0    ignored=0

INFO     Running tox > converge

PLAY [Converge] ****************************************************************

TASK [Gathering Facts] *********************************************************
ok: [instance]

TASK [Include dir vector role] *************************************************

TASK [vector-role : Get vector distrib rpm] ************************************
skipping: [instance]

TASK [vector-role : Install vector rpm packages] *******************************
skipping: [instance]

TASK [vector-role : Get vector distrib deb] ************************************
skipping: [instance]

TASK [vector-role : Install vector deb packages] *******************************
skipping: [instance]

TASK [vector-role : Get vector distrib rpm based for dnf packet manager] *******
changed: [instance]

TASK [vector-role : Install vector packages (dnf packet manager)] **************
changed: [instance]

TASK [vector-role : Generate vector config] ************************************
changed: [instance]

RUNNING HANDLER [vector-role : restart vector service] *************************
changed: [instance]

PLAY RECAP *********************************************************************
instance                   : ok=5    changed=4    unreachable=0    failed=0    skipped=4    rescued=0    ignored=0

INFO     Running tox > destroy

PLAY [Destroy] *****************************************************************

TASK [Destroy molecule instance(s)] ********************************************
changed: [localhost] => (item={'image': 'quay.io/centos/centos:stream8', 'name': 'instance', 'pre_build_image': True})

TASK [Wait for instance(s) deletion to complete] *******************************
FAILED - RETRYING: Wait for instance(s) deletion to complete (300 retries left).
FAILED - RETRYING: Wait for instance(s) deletion to complete (299 retries left).
changed: [localhost] => (item={'started': 1, 'finished': 0, 'ansible_job_id': '468708533956.1469', 'results_file': '/root/.ansible_async/468708533956.1469', 'changed': True, 'failed': False, 'item': {'image': 'quay.io/centos/centos:stream8', 'name': 'instance', 'pre_build_image': True}, 'ansible_loop_var': 'item'})

PLAY RECAP *********************************************************************
localhost                  : ok=2    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

INFO     Pruning extra files from scenario ephemeral directory
py37-ansible30 installed: ansible==3.0.0,ansible-base==2.10.17,ansible-compat==1.0.0,arrow==1.2.3,bcrypt==4.1.2,binaryornot==0.4.4,cached-property==1.5.2,Cerberus==1.3.5,certifi==2024.2.2,cffi==1.15.1,chardet==5.2.0,charset-normalizer==3.3.2,click==8.1.7,click-help-colors==0.9.4,cookiecutter==2.6.0,cryptography==42.0.5,distro==1.9.0,enrich==1.2.7,idna==3.6,importlib-metadata==6.7.0,Jinja2==3.1.3,jmespath==1.0.1,lxml==5.1.0,markdown-it-py==2.2.0,MarkupSafe==2.1.5,mdurl==0.1.2,molecule==3.6.1,molecule-podman==1.1.0,packaging==24.0,paramiko==2.12.0,pluggy==1.2.0,pycparser==2.21,Pygments==2.17.2,PyNaCl==1.5.0,python-dateutil==2.9.0.post0,python-slugify==8.0.4,PyYAML==6.0.1,requests==2.31.0,rich==13.7.1,selinux==0.2.1,six==1.16.0,subprocess-tee==0.3.5,text-unidecode==1.3,typing_extensions==4.7.1,urllib3==2.0.7,zipp==3.15.0
py37-ansible30 run-test-pre: PYTHONHASHSEED='557455390'
py37-ansible30 run-test: commands[0] | molecule test -s tox --destroy always
INFO     tox scenario test matrix: destroy, create, converge, destroy
INFO     Performing prerun...
INFO     Set ANSIBLE_LIBRARY=/root/.cache/ansible-compat/b984a4/modules:/root/.ansible/plugins/modules:/usr/share/ansible/plugins/modules
INFO     Set ANSIBLE_COLLECTIONS_PATH=/root/.cache/ansible-compat/b984a4/collections:/root/.ansible/collections:/usr/share/ansible/collections
INFO     Set ANSIBLE_ROLES_PATH=/root/.cache/ansible-compat/b984a4/roles:/root/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles
INFO     Using /root/.ansible/roles/my_galaxy_namespace.my_name symlink to current repository in order to enable Ansible to find the role using its expected full name.
INFO     Running tox > destroy
INFO     Sanity checks: 'podman'

PLAY [Destroy] *****************************************************************

TASK [Destroy molecule instance(s)] ********************************************
changed: [localhost] => (item={'image': 'quay.io/centos/centos:stream8', 'name': 'instance', 'pre_build_image': True})

TASK [Wait for instance(s) deletion to complete] *******************************
changed: [localhost] => (item={'started': 1, 'finished': 0, 'ansible_job_id': '122809420702.1609', 'results_file': '/root/.ansible_async/122809420702.1609', 'changed': True, 'failed': False, 'item': {'image': 'quay.io/centos/centos:stream8', 'name': 'instance', 'pre_build_image': True}, 'ansible_loop_var': 'item'})

PLAY RECAP *********************************************************************
localhost                  : ok=2    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

INFO     Running tox > create

PLAY [Create] ******************************************************************

TASK [get podman executable path] **********************************************
ok: [localhost]

TASK [save path to executable as fact] *****************************************
ok: [localhost]

TASK [Log into a container registry] *******************************************
skipping: [localhost] => (item="instance registry username: None specified") 

TASK [Check presence of custom Dockerfiles] ************************************
ok: [localhost] => (item=Dockerfile: None specified)

TASK [Create Dockerfiles from image names] *************************************
skipping: [localhost] => (item="Dockerfile: None specified; Image: quay.io/centos/centos:stream8") 

TASK [Discover local Podman images] ********************************************
ok: [localhost] => (item=instance)

TASK [Build an Ansible compatible image] ***************************************
skipping: [localhost] => (item=quay.io/centos/centos:stream8) 

TASK [Determine the CMD directives] ********************************************
ok: [localhost] => (item="instance command: None specified")

TASK [Remove possible pre-existing containers] *********************************
changed: [localhost]

TASK [Discover local podman networks] ******************************************
skipping: [localhost] => (item=instance: None specified) 

TASK [Create podman network dedicated to this scenario] ************************
skipping: [localhost]

TASK [Create molecule instance(s)] *********************************************
changed: [localhost] => (item=instance)

TASK [Wait for instance(s) creation to complete] *******************************
changed: [localhost] => (item=instance)

PLAY RECAP *********************************************************************
localhost                  : ok=8    changed=3    unreachable=0    failed=0    skipped=5    rescued=0    ignored=0

INFO     Running tox > converge

PLAY [Converge] ****************************************************************

TASK [Gathering Facts] *********************************************************
ok: [instance]

TASK [Include dir vector role] *************************************************

TASK [vector-role : Get vector distrib rpm] ************************************
skipping: [instance]

TASK [vector-role : Install vector rpm packages] *******************************
skipping: [instance]

TASK [vector-role : Get vector distrib deb] ************************************
skipping: [instance]

TASK [vector-role : Install vector deb packages] *******************************
skipping: [instance]

TASK [vector-role : Get vector distrib rpm based for dnf packet manager] *******
changed: [instance]

TASK [vector-role : Install vector packages (dnf packet manager)] **************
changed: [instance]

TASK [vector-role : Generate vector config] ************************************
changed: [instance]

RUNNING HANDLER [vector-role : restart vector service] *************************
changed: [instance]

PLAY RECAP *********************************************************************
instance                   : ok=5    changed=4    unreachable=0    failed=0    skipped=4    rescued=0    ignored=0

INFO     Running tox > destroy

PLAY [Destroy] *****************************************************************

TASK [Destroy molecule instance(s)] ********************************************
changed: [localhost] => (item={'image': 'quay.io/centos/centos:stream8', 'name': 'instance', 'pre_build_image': True})

TASK [Wait for instance(s) deletion to complete] *******************************
FAILED - RETRYING: Wait for instance(s) deletion to complete (300 retries left).
FAILED - RETRYING: Wait for instance(s) deletion to complete (299 retries left).
changed: [localhost] => (item={'started': 1, 'finished': 0, 'ansible_job_id': '37314159519.2745', 'results_file': '/root/.ansible_async/37314159519.2745', 'changed': True, 'failed': False, 'item': {'image': 'quay.io/centos/centos:stream8', 'name': 'instance', 'pre_build_image': True}, 'ansible_loop_var': 'item'})

PLAY RECAP *********************************************************************
localhost                  : ok=2    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

INFO     Pruning extra files from scenario ephemeral directory
py39-ansible212 create: /opt/vector-role/.tox/py39-ansible212
py39-ansible212 installdeps: -rtox-requirements.txt, ansible<3.0
py39-ansible212 installed: ansible==2.10.7,ansible-base==2.10.17,ansible-compat==4.1.11,ansible-core==2.15.9,ansible-lint==5.1.3,arrow==1.3.0,attrs==23.2.0,bcrypt==4.1.2,binaryornot==0.4.4,bracex==2.4,Cerberus==1.3.5,certifi==2024.2.2,cffi==1.16.0,chardet==5.2.0,charset-normalizer==3.3.2,click==8.1.7,click-help-colors==0.9.4,cookiecutter==2.6.0,cryptography==42.0.5,distro==1.9.0,enrich==1.2.7,idna==3.6,importlib-resources==5.0.7,Jinja2==3.1.3,jmespath==1.0.1,jsonschema==4.21.1,jsonschema-specifications==2023.12.1,lxml==5.1.0,markdown-it-py==3.0.0,MarkupSafe==2.1.5,mdurl==0.1.2,molecule==3.5.2,molecule-podman==2.0.0,packaging==24.0,paramiko==2.12.0,pathspec==0.12.1,pluggy==1.4.0,pycparser==2.21,Pygments==2.17.2,PyNaCl==1.5.0,python-dateutil==2.9.0.post0,python-slugify==8.0.4,PyYAML==5.4.1,referencing==0.34.0,requests==2.31.0,resolvelib==1.0.1,rich==13.7.1,rpds-py==0.18.0,ruamel.yaml==0.18.6,ruamel.yaml.clib==0.2.8,selinux==0.3.0,six==1.16.0,subprocess-tee==0.4.1,tenacity==8.2.3,text-unidecode==1.3,types-python-dateutil==2.9.0.20240316,typing_extensions==4.10.0,urllib3==2.2.1,wcmatch==8.5.1,yamllint==1.26.3
py39-ansible212 run-test-pre: PYTHONHASHSEED='557455390'
py39-ansible212 run-test: commands[0] | molecule test -s tox --destroy always
INFO     tox scenario test matrix: destroy, create, converge, destroy
INFO     Performing prerun...
INFO     Running tox > destroy
INFO     Sanity checks: 'podman'
Traceback (most recent call last):
  File "/opt/vector-role/.tox/py39-ansible212/bin/molecule", line 8, in <module>
    sys.exit(main())
  File "/opt/vector-role/.tox/py39-ansible212/lib/python3.9/site-packages/click/core.py", line 1157, in __call__
    return self.main(*args, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible212/lib/python3.9/site-packages/click/core.py", line 1078, in main
    rv = self.invoke(ctx)
  File "/opt/vector-role/.tox/py39-ansible212/lib/python3.9/site-packages/click/core.py", line 1688, in invoke
    return _process_result(sub_ctx.command.invoke(sub_ctx))
  File "/opt/vector-role/.tox/py39-ansible212/lib/python3.9/site-packages/click/core.py", line 1434, in invoke
    return ctx.invoke(self.callback, **ctx.params)
  File "/opt/vector-role/.tox/py39-ansible212/lib/python3.9/site-packages/click/core.py", line 783, in invoke
    return __callback(*args, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible212/lib/python3.9/site-packages/click/decorators.py", line 33, in new_func
    return f(get_current_context(), *args, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible212/lib/python3.9/site-packages/molecule/command/test.py", line 159, in test
    base.execute_cmdline_scenarios(scenario_name, args, command_args, ansible_args)
  File "/opt/vector-role/.tox/py39-ansible212/lib/python3.9/site-packages/molecule/command/base.py", line 118, in execute_cmdline_scenarios
    execute_scenario(scenario)
  File "/opt/vector-role/.tox/py39-ansible212/lib/python3.9/site-packages/molecule/command/base.py", line 160, in execute_scenario
    execute_subcommand(scenario.config, action)
  File "/opt/vector-role/.tox/py39-ansible212/lib/python3.9/site-packages/molecule/command/base.py", line 149, in execute_subcommand
    return command(config).execute()
  File "/opt/vector-role/.tox/py39-ansible212/lib/python3.9/site-packages/molecule/logger.py", line 188, in wrapper
    rt = func(*args, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible212/lib/python3.9/site-packages/molecule/command/destroy.py", line 107, in execute
    self._config.provisioner.destroy()
  File "/opt/vector-role/.tox/py39-ansible212/lib/python3.9/site-packages/molecule/provisioner/ansible.py", line 705, in destroy
    pb.execute()
  File "/opt/vector-role/.tox/py39-ansible212/lib/python3.9/site-packages/molecule/provisioner/ansible_playbook.py", line 110, in execute
    self._config.driver.sanity_checks()
  File "/opt/vector-role/.tox/py39-ansible212/lib/python3.9/site-packages/molecule_podman/driver.py", line 224, in sanity_checks
    if runtime.version < Version("2.10.0"):
  File "/opt/vector-role/.tox/py39-ansible212/lib/python3.9/site-packages/ansible_compat/runtime.py", line 413, in version
    self._version = parse_ansible_version(proc.stdout)
  File "/opt/vector-role/.tox/py39-ansible212/lib/python3.9/site-packages/ansible_compat/config.py", line 44, in parse_ansible_version
    raise InvalidPrerequisiteError(msg)
ansible_compat.errors.InvalidPrerequisiteError: Unable to parse ansible cli version: ansible 2.10.17
  config file = None
  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /opt/vector-role/.tox/py39-ansible212/lib/python3.9/site-packages/ansible
  executable location = /opt/vector-role/.tox/py39-ansible212/bin/ansible
  python version = 3.9.2 (default, Jun 13 2022, 19:42:33) [GCC 8.5.0 20210514 (Red Hat 8.5.0-10)]

Keep in mind that only 2.12 or newer are supported.
ERROR: InvocationError for command /opt/vector-role/.tox/py39-ansible212/bin/molecule test -s tox --destroy always (exited with code 1)
py39-ansible30 installed: ansible==3.0.0,ansible-base==2.10.17,ansible-compat==4.1.11,ansible-core==2.15.9,attrs==23.2.0,bracex==2.4,cffi==1.16.0,click==8.1.7,click-help-colors==0.9.4,cryptography==42.0.5,distro==1.9.0,enrich==1.2.7,importlib-resources==5.0.7,Jinja2==3.1.3,jmespath==1.0.1,jsonschema==4.21.1,jsonschema-specifications==2023.12.1,lxml==5.1.0,markdown-it-py==3.0.0,MarkupSafe==2.1.5,mdurl==0.1.2,molecule==6.0.3,molecule-podman==2.0.3,packaging==24.0,pluggy==1.4.0,pycparser==2.21,Pygments==2.17.2,PyYAML==6.0.1,referencing==0.34.0,resolvelib==1.0.1,rich==13.7.1,rpds-py==0.18.0,selinux==0.3.0,subprocess-tee==0.4.1,typing_extensions==4.10.0,wcmatch==8.5.1
py39-ansible30 run-test-pre: PYTHONHASHSEED='557455390'
py39-ansible30 run-test: commands[0] | molecule test -s tox --destroy always
WARNING  Driver podman does not provide a schema.
INFO     tox scenario test matrix: destroy, create, converge, destroy
INFO     Performing prerun with role_name_check=1...
ERROR    CompletedProcess(args=['ansible-galaxy', 'collection', 'list', '--format=json'], returncode=250, stdout='the full traceback was:\n\nTraceback (most recent call last):\n  File "/opt/vector-role/.tox/py39-ansible30/bin/ansible-galaxy", line 92, in <module>\n    mycli = getattr(__import__("ansible.cli.%s" % sub, fromlist=), myclass)\n  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/ansible/cli/galaxy.py", line 24, in <module>\n    from ansible.galaxy.collection import (\n  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/ansible/galaxy/collection/__init__.py", line 90, in <module>\n    from ansible.galaxy.collection.concrete_artifact_manager import (\n  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/ansible/galaxy/collection/concrete_artifact_manager.py", line 30, in <module>\n    from ansible.galaxy.api import should_retry_error\nImportError: cannot import name \'should_retry_error\' from \'ansible.galaxy.api\' (/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/ansible/galaxy/api.py)\n', stderr="ERROR! Unexpected Exception, this is probably a bug: cannot import name 'should_retry_error' from 'ansible.galaxy.api' (/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/ansible/galaxy/api.py)\n")
Traceback (most recent call last):
  File "/opt/vector-role/.tox/py39-ansible30/bin/molecule", line 8, in <module>
    sys.exit(main())
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/click/core.py", line 1157, in __call__
    return self.main(*args, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/click/core.py", line 1078, in main
    rv = self.invoke(ctx)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/click/core.py", line 1688, in invoke
    return _process_result(sub_ctx.command.invoke(sub_ctx))
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/click/core.py", line 1434, in invoke
    return ctx.invoke(self.callback, **ctx.params)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/click/core.py", line 783, in invoke
    return __callback(*args, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/click/decorators.py", line 33, in new_func
    return f(get_current_context(), *args, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/molecule/command/test.py", line 113, in test
    base.execute_cmdline_scenarios(scenario_name, args, command_args, ansible_args)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/molecule/command/base.py", line 113, in execute_cmdline_scenarios
    scenario.config.runtime.prepare_environment(
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/ansible_compat/runtime.py", line 684, in prepare_environment
    self.load_collections()
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/ansible_compat/runtime.py", line 285, in load_collections
    raise RuntimeError(msg)
RuntimeError: Unable to list collections: CompletedProcess(args=['ansible-galaxy', 'collection', 'list', '--format=json'], returncode=250, stdout='the full traceback was:\n\nTraceback (most recent call last):\n  File "/opt/vector-role/.tox/py39-ansible30/bin/ansible-galaxy", line 92, in <module>\n    mycli = getattr(__import__("ansible.cli.%s" % sub, fromlist=[myclass]), myclass)\n  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/ansible/cli/galaxy.py", line 24, in <module>\n    from ansible.galaxy.collection import (\n  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/ansible/galaxy/collection/__init__.py", line 90, in <module>\n    from ansible.galaxy.collection.concrete_artifact_manager import (\n  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/ansible/galaxy/collection/concrete_artifact_manager.py", line 30, in <module>\n    from ansible.galaxy.api import should_retry_error\nImportError: cannot import name \'should_retry_error\' from \'ansible.galaxy.api\' (/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/ansible/galaxy/api.py)\n', stderr="ERROR! Unexpected Exception, this is probably a bug: cannot import name 'should_retry_error' from 'ansible.galaxy.api' (/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/ansible/galaxy/api.py)\n")
ERROR: InvocationError for command /opt/vector-role/.tox/py39-ansible30/bin/molecule test -s tox --destroy always (exited with code 1)
______________________________________________________________________ summary ______________________________________________________________________
  py37-ansible212: commands succeeded
  py37-ansible30: commands succeeded
ERROR:   py39-ansible212: commands failed
ERROR:   py39-ansible30: commands failed
```
### 7   
https://github.com/suntsovvv/vector-role/releases/tag/v1.1.1


