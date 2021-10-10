# Основная часть
```
1. 
TASK [Print fact] *****************************************************************************************************************
ok: [localhost] => {
    "msg": 12
}
```
```
2.
TASK [Print fact] *****************************************************************************************************************
ok: [localhost] => {
    "msg": "all default fact"
}
```
```
4.
TASK [Print fact] *****************************************************************************************************************
ok: [centos7] => {
    "msg": "el"
}
ok: [ubuntu] => {
    "msg": "deb"
}
```
```
6.
TASK [Print fact] *****************************************************************************************************************
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}
```
```
7.
ansible-vault encrypt group_vars/deb/examp.yml
New Vault password:
Confirm New Vault password:
Encryption successful
```
```
ansible-vault encrypt group_vars/el/examp.yml
New Vault password:
Confirm New Vault password:
Encryption successful
```
```
8.
ansible-playbook site.yml -i inventory/prod.yml --ask-vault-pass
Vault password:

PLAY [Print os facts] *************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] *******************************************************************************************************************
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] *****************************************************************************************************************
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}

PLAY RECAP ************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```
```
9.
ansible-doc -t connection -l
local                          execute on controller
```
```
10.
---
  el:
    hosts:
      centos7:
        ansible_connection: docker
  deb:
    hosts:
      ubuntu:
        ansible_connection: docker
  local:
    hosts:
      localhost:
        ansible_connection: local
```
```
11.
 ansible-playbook site.yml -i inventory/prod.yml --ask-vault-pass
Vault password:

PLAY [Print os facts] *************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************
ok: [localhost]
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] *******************************************************************************************************************
ok: [localhost] => {
    "msg": "Ubuntu"
}
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] *****************************************************************************************************************
ok: [localhost] => {
    "msg": "all default fact"
}
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}

PLAY RECAP ************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```
# Самоконтроль выполненения задания

```
1. Где расположен файл с `some_fact` из второго пункта задания?
```
- group_vars/all/examp.yml
```
2. Какая команда нужна для запуска вашего `playbook` на окружении `test.yml`?
```
- ansible-playbook -i inventory/test.yml site.yml
```
3. Какой командой можно зашифровать файл?
```
- ansible-vault encrypt path/to/file
```
4. Какой командой можно расшифровать файл?
```
- aansible-vault decrypt path/to/file
```
5. Можно ли посмотреть содержимое зашифрованного файла без команды расшифровки файла? Если можно, то как?
```
- ansible-vault view path/to/file
```
6. Как выглядит команда запуска `playbook`, если переменные зашифрованы?
```
- ansible-playbook -i inventory/prod.yml site.yml --ask-vault-password
```
7. Как называется модуль подключения к host на windows?
```
- winrm
```
8. Приведите полный текст команды для поиска информации в документации ansible для модуля подключений ssh
```
- ansible-doc -t connection ssh
```
9. Какой параметр из модуля подключения `ssh` необходим для того, чтобы определить пользователя, под которым необходимо совершать подключение?
```
- remote_user
