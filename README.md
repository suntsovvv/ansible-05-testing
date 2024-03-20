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
