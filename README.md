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

