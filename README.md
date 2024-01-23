# Домашнее задание к занятию 5 «Тестирование roles» - Сергей Ситкарёв

## Molecule

1. Запустите molecule test -s ubuntu_xenial (или с любым другим сценарием, не имеет значения) внутри корневой директории clickhouse-role, посмотрите на вывод команды. Данная команда может отработать с ошибками или не отработать вовсе, это нормально. Наша цель - посмотреть как другие в реальном мире используют молекулу И из чего может состоять сценарий тестирования.

![Задание1](https://github.com/SSitkarev/ansible-05/blob/main/img/1.jpg)

2. Перейдите в каталог с ролью vector-role и создайте сценарий тестирования по умолчанию при помощи molecule init scenario --driver-name docker.

![Задание2](https://github.com/SSitkarev/ansible-05/blob/main/img/2.jpg)

3. Добавьте несколько разных дистрибутивов (oraclelinux:8, ubuntu:latest) для инстансов и протестируйте роль, исправьте найденные ошибки, если они есть.

<details>
  <summary>molecule test 1</summary>

(.venv) ssco@Ansible:~/ansible/ansible-05/roles/vector_role$ molecule test
WARNING  The scenario config file ('/home/ssco/ansible/ansible-05/roles/vector_role/molecule/default/molecule.yml') has been modified since the scenario was created. If recent changes are important, reset the scenario with 'molecule destroy' to clean up created items or 'molecule reset' to clear current configuration.
WARNING  Driver docker does not provide a schema.
INFO     default scenario test matrix: dependency, cleanup, destroy, syntax, create, prepare, converge, idempotence, side_effect, verify, cleanup, destroy
INFO     Performing prerun with role_name_check=1...
WARNING  Computed fully qualified role name of vector_role does not follow current galaxy requirements.
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
INFO     Sanity checks: 'docker'

PLAY [Destroy] *****************************************************************

TASK [Populate instance config] ************************************************
ok: [localhost]

TASK [Dump instance config] ****************************************************
skipping: [localhost]

PLAY RECAP *********************************************************************
localhost                  : ok=1    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0

INFO     Running default > syntax

playbook: /home/ssco/ansible/ansible-05/roles/vector_role/molecule/default/converge.yml
INFO     Running default > create

PLAY [Create] ******************************************************************

TASK [Populate instance config dict] *******************************************
skipping: [localhost]

TASK [Convert instance config dict to a list] **********************************
skipping: [localhost]

TASK [Dump instance config] ****************************************************
skipping: [localhost]

PLAY RECAP *********************************************************************
localhost                  : ok=0    changed=0    unreachable=0    failed=0    skipped=3    rescued=0    ignored=0

INFO     Running default > prepare
WARNING  Skipping, prepare playbook not configured.
INFO     Running default > converge

PLAY [Converge] ****************************************************************

TASK [Replace this task with one that validates your content] ******************
ok: [oraclelinux] => {
    "msg": "This is the effective test"
}
ok: [ubuntu:latest] => {
    "msg": "This is the effective test"
}

PLAY RECAP *********************************************************************
oraclelinux                : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ubuntu:latest              : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

INFO     Running default > idempotence

PLAY [Converge] ****************************************************************

TASK [Replace this task with one that validates your content] ******************
ok: [oraclelinux] => {
    "msg": "This is the effective test"
}
ok: [ubuntu:latest] => {
    "msg": "This is the effective test"
}

PLAY RECAP *********************************************************************
oraclelinux                : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ubuntu:latest              : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

INFO     Idempotence completed successfully.
INFO     Running default > side_effect
WARNING  Skipping, side effect playbook not configured.
INFO     Running default > verify
INFO     Running Ansible Verifier
WARNING  Skipping, verify action has no playbook.
INFO     Verifier completed successfully.
INFO     Running default > cleanup
WARNING  Skipping, cleanup playbook not configured.
INFO     Running default > destroy

PLAY [Destroy] *****************************************************************

TASK [Populate instance config] ************************************************
ok: [localhost]

TASK [Dump instance config] ****************************************************
skipping: [localhost]

PLAY RECAP *********************************************************************
localhost                  : ok=1    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0

INFO     Pruning extra files from scenario ephemeral directory

</details>

4. Добавьте несколько assert в verify.yml-файл для проверки работоспособности vector-role (проверка, что конфиг валидный, проверка успешности запуска и др.).

5. Запустите тестирование роли повторно и проверьте, что оно прошло успешно.

<details>
  <summary>molecule test 2</summary>
  
(.venv) ssco@Ansible:~/ansible/ansible-05/roles/vector_role$ molecule test
WARNING  Driver docker does not provide a schema.
INFO     default scenario test matrix: dependency, cleanup, destroy, syntax, create, prepare, converge, idempotence, side_effect, verify, cleanup, destroy
INFO     Performing prerun with role_name_check=1...
WARNING  Computed fully qualified role name of vector_role does not follow current galaxy requirements.
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
INFO     Sanity checks: 'docker'

PLAY [Destroy] *****************************************************************

TASK [Populate instance config] ************************************************
ok: [localhost]

TASK [Dump instance config] ****************************************************
skipping: [localhost]

PLAY RECAP *********************************************************************
localhost                  : ok=1    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0

INFO     Running default > syntax

playbook: /home/ssco/ansible/ansible-05/roles/vector_role/molecule/default/converge.yml
INFO     Running default > create

PLAY [Create] ******************************************************************

TASK [Populate instance config dict] *******************************************
skipping: [localhost]

TASK [Convert instance config dict to a list] **********************************
skipping: [localhost]

TASK [Dump instance config] ****************************************************
skipping: [localhost]

PLAY RECAP *********************************************************************
localhost                  : ok=0    changed=0    unreachable=0    failed=0    skipped=3    rescued=0    ignored=0

INFO     Running default > prepare
WARNING  Skipping, prepare playbook not configured.
INFO     Running default > converge

PLAY [Converge] ****************************************************************

TASK [Replace this task with one that validates your content] ******************
ok: [oraclelinux] => {
    "msg": "This is the effective test"
}
ok: [ubuntu:latest] => {
    "msg": "This is the effective test"
}

PLAY RECAP *********************************************************************
oraclelinux                : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ubuntu:latest              : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

INFO     Running default > idempotence

PLAY [Converge] ****************************************************************

TASK [Replace this task with one that validates your content] ******************
ok: [oraclelinux] => {
    "msg": "This is the effective test"
}
ok: [ubuntu:latest] => {
    "msg": "This is the effective test"
}

PLAY RECAP *********************************************************************
oraclelinux                : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ubuntu:latest              : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

INFO     Idempotence completed successfully.
INFO     Running default > side_effect
WARNING  Skipping, side effect playbook not configured.
INFO     Running default > verify
INFO     Running Ansible Verifier
WARNING  Skipping, verify action has no playbook.
INFO     Verifier completed successfully.
INFO     Running default > cleanup
WARNING  Skipping, cleanup playbook not configured.
INFO     Running default > destroy

PLAY [Destroy] *****************************************************************

TASK [Populate instance config] ************************************************
ok: [localhost]

TASK [Dump instance config] ****************************************************
skipping: [localhost]

PLAY RECAP *********************************************************************
localhost                  : ok=1    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0

INFO     Pruning extra files from scenario ephemeral directory

</details>

6. Добавьте новый тег на коммит с рабочим сценарием в соответствии с семантическим версионированием.

[Release 1.0.0](https://github.com/SSitkarev/vector_role/tree/1.0.0)

## Tox

1. Добавьте в директорию с vector-role файлы из директории.

2. Запустите docker run --privileged=True -v <path_to_repo>:/opt/vector-role -w /opt/vector-role -it aragast/netology:latest /bin/bash, где path_to_repo — путь до корня репозитория с vector-role на вашей файловой системе.

3. Внутри контейнера выполните команду tox, посмотрите на вывод.

<details>
  <summary>Tox 1</summary>
  
(.venv) ssco@Ansible:~/ansible/ansible-05/roles/vector_role$ docker run --privileged=True -v ~/ansible/ansible-05/roles/vector_role:/opt/vector-role -w /opt/vector-role -it aragast/netology:latest /bin/bash
[root@dd2bc7efc31c vector-role]# tox
py37-ansible210 create: /opt/vector-role/.tox/py37-ansible210
py37-ansible210 installdeps: -rtox-requirements.txt, ansible<3.0
py37-ansible210 installed: ansible==2.10.7,ansible-base==2.10.17,ansible-compat==1.0.0,arrow==1.2.3,bcrypt==4.1.2,binaryornot==0.4.4,cached-property==1.5.2,Cerberus==1.3.5,certifi==2023.11.17,cffi==1.15.1,chardet==5.2.0,charset-normalizer==3.3.2,click==8.1.7,click-help-colors==0.9.4,cookiecutter==2.5.0,cryptography==42.0.0,distro==1.9.0,enrich==1.2.7,idna==3.6,importlib-metadata==6.7.0,Jinja2==3.1.3,jmespath==1.0.1,lxml==5.1.0,markdown-it-py==2.2.0,MarkupSafe==2.1.4,mdurl==0.1.2,molecule==3.6.1,molecule-podman==1.1.0,packaging==23.2,paramiko==2.12.0,pluggy==1.2.0,pycparser==2.21,Pygments==2.17.2,PyNaCl==1.5.0,python-dateutil==2.8.2,python-slugify==8.0.1,PyYAML==6.0.1,requests==2.31.0,rich==13.7.0,selinux==0.2.1,six==1.16.0,subprocess-tee==0.3.5,text-unidecode==1.3,typing_extensions==4.7.1,urllib3==2.0.7,zipp==3.15.0
py37-ansible210 run-test-pre: PYTHONHASHSEED='1575294448'
py37-ansible210 run-test: commands[0] | molecule test -s compatibility --destroy always
CRITICAL 'molecule/compatibility/molecule.yml' glob failed.  Exiting.
ERROR: InvocationError for command /opt/vector-role/.tox/py37-ansible210/bin/molecule test -s compatibility --destroy always (exited with code 1)
py37-ansible30 create: /opt/vector-role/.tox/py37-ansible30
py37-ansible30 installdeps: -rtox-requirements.txt, ansible<3.1
py37-ansible30 installed: ansible==3.0.0,ansible-base==2.10.17,ansible-compat==1.0.0,arrow==1.2.3,bcrypt==4.1.2,binaryornot==0.4.4,cached-property==1.5.2,Cerberus==1.3.5,certifi==2023.11.17,cffi==1.15.1,chardet==5.2.0,charset-normalizer==3.3.2,click==8.1.7,click-help-colors==0.9.4,cookiecutter==2.5.0,cryptography==42.0.0,distro==1.9.0,enrich==1.2.7,idna==3.6,importlib-metadata==6.7.0,Jinja2==3.1.3,jmespath==1.0.1,lxml==5.1.0,markdown-it-py==2.2.0,MarkupSafe==2.1.4,mdurl==0.1.2,molecule==3.6.1,molecule-podman==1.1.0,packaging==23.2,paramiko==2.12.0,pluggy==1.2.0,pycparser==2.21,Pygments==2.17.2,PyNaCl==1.5.0,python-dateutil==2.8.2,python-slugify==8.0.1,PyYAML==6.0.1,requests==2.31.0,rich==13.7.0,selinux==0.2.1,six==1.16.0,subprocess-tee==0.3.5,text-unidecode==1.3,typing_extensions==4.7.1,urllib3==2.0.7,zipp==3.15.0
py37-ansible30 run-test-pre: PYTHONHASHSEED='1575294448'
py37-ansible30 run-test: commands[0] | molecule test -s compatibility --destroy always
CRITICAL 'molecule/compatibility/molecule.yml' glob failed.  Exiting.
ERROR: InvocationError for command /opt/vector-role/.tox/py37-ansible30/bin/molecule test -s compatibility --destroy always (exited with code 1)
py39-ansible210 create: /opt/vector-role/.tox/py39-ansible210
py39-ansible210 installdeps: -rtox-requirements.txt, ansible<3.0
py39-ansible210 installed: ansible==2.10.7,ansible-base==2.10.17,ansible-compat==4.1.11,ansible-core==2.15.8,attrs==23.2.0,bracex==2.4,cffi==1.16.0,click==8.1.7,click-help-colors==0.9.4,cryptography==42.0.0,distro==1.9.0,enrich==1.2.7,importlib-resources==5.0.7,Jinja2==3.1.3,jmespath==1.0.1,jsonschema==4.21.1,jsonschema-specifications==2023.12.1,lxml==5.1.0,markdown-it-py==3.0.0,MarkupSafe==2.1.4,mdurl==0.1.2,molecule==6.0.3,molecule-podman==2.0.3,packaging==23.2,pluggy==1.3.0,pycparser==2.21,Pygments==2.17.2,PyYAML==6.0.1,referencing==0.32.1,resolvelib==1.0.1,rich==13.7.0,rpds-py==0.17.1,selinux==0.3.0,subprocess-tee==0.4.1,typing_extensions==4.9.0,wcmatch==8.5
py39-ansible210 run-test-pre: PYTHONHASHSEED='1575294448'
py39-ansible210 run-test: commands[0] | molecule test -s compatibility --destroy always
CRITICAL 'molecule/compatibility/molecule.yml' glob failed.  Exiting.
ERROR: InvocationError for command /opt/vector-role/.tox/py39-ansible210/bin/molecule test -s compatibility --destroy always (exited with code 1)
py39-ansible30 create: /opt/vector-role/.tox/py39-ansible30
py39-ansible30 installdeps: -rtox-requirements.txt, ansible<3.1
py39-ansible30 installed: ansible==3.0.0,ansible-base==2.10.17,ansible-compat==4.1.11,ansible-core==2.15.8,attrs==23.2.0,bracex==2.4,cffi==1.16.0,click==8.1.7,click-help-colors==0.9.4,cryptography==42.0.0,distro==1.9.0,enrich==1.2.7,importlib-resources==5.0.7,Jinja2==3.1.3,jmespath==1.0.1,jsonschema==4.21.1,jsonschema-specifications==2023.12.1,lxml==5.1.0,markdown-it-py==3.0.0,MarkupSafe==2.1.4,mdurl==0.1.2,molecule==6.0.3,molecule-podman==2.0.3,packaging==23.2,pluggy==1.3.0,pycparser==2.21,Pygments==2.17.2,PyYAML==6.0.1,referencing==0.32.1,resolvelib==1.0.1,rich==13.7.0,rpds-py==0.17.1,selinux==0.3.0,subprocess-tee==0.4.1,typing_extensions==4.9.0,wcmatch==8.5
py39-ansible30 run-test-pre: PYTHONHASHSEED='1575294448'
py39-ansible30 run-test: commands[0] | molecule test -s compatibility --destroy always
CRITICAL 'molecule/compatibility/molecule.yml' glob failed.  Exiting.
ERROR: InvocationError for command /opt/vector-role/.tox/py39-ansible30/bin/molecule test -s compatibility --destroy always (exited with code 1)
_______________________________________________________________________ summary ________________________________________________________________________
ERROR:   py37-ansible210: commands failed
ERROR:   py37-ansible30: commands failed
ERROR:   py39-ansible210: commands failed
ERROR:   py39-ansible30: commands failed
  
</details>  

4. Создайте облегчённый сценарий для molecule с драйвером molecule_podman. Проверьте его на исполнимость.

5. Пропишите правильную команду в tox.ini, чтобы запускался облегчённый сценарий.

6. Запустите команду tox. Убедитесь, что всё отработало успешно.

Всё настроил, однако почему-то ansible не удаётся определить имя роли.
_WARNING  Computed fully qualified role name of vector_role does not follow current galaxy requirements._

В первом задании это удалось обойти при помощи параметра _role_name_check: 1_

Однако при использовании Tox этот параметр не помогает.

пробовал править meta/main.yml файл различными вариантами - не помогает. Версия ansible core 2.16.2

_Computed fully qualified role name of vector_role does not follow current galaxy requirements_


<details>
  <summary>Tox2</summary>
  
(.venv) ssco@Ansible:~/ansible/ansible-05/roles/vector_role$ docker run --privileged=True -v ~/ansible/ansible-05/roles/vector_role:/opt/vector-role -w /opt/vector-role -it aragast/netology:latest /bin/bash
[root@ca6d28680071 vector-role]# tox
py37-ansible210 installed: ansible==2.10.7,ansible-base==2.10.17,ansible-compat==1.0.0,arrow==1.2.3,bcrypt==4.1.2,binaryornot==0.4.4,cached-property==1.5.2,Cerberus==1.3.5,certifi==2023.11.17,cffi==1.15.1,chardet==5.2.0,charset-normalizer==3.3.2,click==8.1.7,click-help-colors==0.9.4,cookiecutter==2.5.0,cryptography==42.0.0,distro==1.9.0,enrich==1.2.7,idna==3.6,importlib-metadata==6.7.0,Jinja2==3.1.3,jmespath==1.0.1,lxml==5.1.0,markdown-it-py==2.2.0,MarkupSafe==2.1.4,mdurl==0.1.2,molecule==3.6.1,molecule-podman==1.1.0,packaging==23.2,paramiko==2.12.0,pluggy==1.2.0,pycparser==2.21,Pygments==2.17.2,PyNaCl==1.5.0,python-dateutil==2.8.2,python-slugify==8.0.1,PyYAML==6.0.1,requests==2.31.0,rich==13.7.0,selinux==0.2.1,six==1.16.0,subprocess-tee==0.3.5,text-unidecode==1.3,typing_extensions==4.7.1,urllib3==2.0.7,zipp==3.15.0
py37-ansible210 run-test-pre: PYTHONHASHSEED='1669044436'
py37-ansible210 run-test: commands[0] | molecule test -s default --destroy always
INFO     default scenario test matrix: destroy, create, converge, destroy
INFO     Performing prerun...
INFO     Set ANSIBLE_LIBRARY=/root/.cache/ansible-compat/b984a4/modules:/root/.ansible/plugins/modules:/usr/share/ansible/plugins/modules
INFO     Set ANSIBLE_COLLECTIONS_PATH=/root/.cache/ansible-compat/b984a4/collections:/root/.ansible/collections:/usr/share/ansible/collections
INFO     Set ANSIBLE_ROLES_PATH=/root/.cache/ansible-compat/b984a4/roles:/root/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles
ERROR    Computed fully qualified role name of vector_role does not follow current galaxy requirements.
Please edit meta/main.yml and assure we can correctly determine full role name:

galaxy_info:
role_name: my_name  # if absent directory name hosting role is used instead
namespace: my_galaxy_namespace  # if absent, author is used instead

Namespace: https://galaxy.ansible.com/docs/contributing/namespaces.html#galaxy-namespace-limitations
Role: https://galaxy.ansible.com/docs/contributing/creating_role.html#role-names

As an alternative, you can add 'role-name' to either skip_list or warn_list.

Traceback (most recent call last):
  File "/opt/vector-role/.tox/py37-ansible210/bin/molecule", line 8, in <module>
    sys.exit(main())
  File "/opt/vector-role/.tox/py37-ansible210/lib/python3.7/site-packages/click/core.py", line 1157, in __call__
    return self.main(*args, **kwargs)
  File "/opt/vector-role/.tox/py37-ansible210/lib/python3.7/site-packages/click/core.py", line 1078, in main
    rv = self.invoke(ctx)
  File "/opt/vector-role/.tox/py37-ansible210/lib/python3.7/site-packages/click/core.py", line 1688, in invoke
    return _process_result(sub_ctx.command.invoke(sub_ctx))
  File "/opt/vector-role/.tox/py37-ansible210/lib/python3.7/site-packages/click/core.py", line 1434, in invoke
    return ctx.invoke(self.callback, **ctx.params)
  File "/opt/vector-role/.tox/py37-ansible210/lib/python3.7/site-packages/click/core.py", line 783, in invoke
    return __callback(*args, **kwargs)
  File "/opt/vector-role/.tox/py37-ansible210/lib/python3.7/site-packages/click/decorators.py", line 33, in new_func
    return f(get_current_context(), *args, **kwargs)
  File "/opt/vector-role/.tox/py37-ansible210/lib/python3.7/site-packages/molecule/command/test.py", line 161, in test
    base.execute_cmdline_scenarios(scenario_name, args, command_args, ansible_args)
  File "/opt/vector-role/.tox/py37-ansible210/lib/python3.7/site-packages/molecule/command/base.py", line 111, in execute_cmdline_scenarios
    scenario.config.runtime.prepare_environment(install_local=True)
  File "/opt/vector-role/.tox/py37-ansible210/lib/python3.7/site-packages/ansible_compat/runtime.py", line 334, in prepare_environment
    self._install_galaxy_role(self.project_dir, ignore_errors=True)
  File "/opt/vector-role/.tox/py37-ansible210/lib/python3.7/site-packages/ansible_compat/runtime.py", line 478, in _install_galaxy_role
    raise InvalidPrerequisiteError(msg)
ansible_compat.errors.InvalidPrerequisiteError: Computed fully qualified role name of vector_role does not follow current galaxy requirements.
Please edit meta/main.yml and assure we can correctly determine full role name:

galaxy_info:
role_name: my_name  # if absent directory name hosting role is used instead
namespace: my_galaxy_namespace  # if absent, author is used instead

Namespace: https://galaxy.ansible.com/docs/contributing/namespaces.html#galaxy-namespace-limitations
Role: https://galaxy.ansible.com/docs/contributing/creating_role.html#role-names

As an alternative, you can add 'role-name' to either skip_list or warn_list.

ERROR: InvocationError for command /opt/vector-role/.tox/py37-ansible210/bin/molecule test -s default --destroy always (exited with code 1)
py37-ansible30 installed: ansible==3.0.0,ansible-base==2.10.17,ansible-compat==1.0.0,arrow==1.2.3,bcrypt==4.1.2,binaryornot==0.4.4,cached-property==1.5.2,Cerberus==1.3.5,certifi==2023.11.17,cffi==1.15.1,chardet==5.2.0,charset-normalizer==3.3.2,click==8.1.7,click-help-colors==0.9.4,cookiecutter==2.5.0,cryptography==42.0.0,distro==1.9.0,enrich==1.2.7,idna==3.6,importlib-metadata==6.7.0,Jinja2==3.1.3,jmespath==1.0.1,lxml==5.1.0,markdown-it-py==2.2.0,MarkupSafe==2.1.4,mdurl==0.1.2,molecule==3.6.1,molecule-podman==1.1.0,packaging==23.2,paramiko==2.12.0,pluggy==1.2.0,pycparser==2.21,Pygments==2.17.2,PyNaCl==1.5.0,python-dateutil==2.8.2,python-slugify==8.0.1,PyYAML==6.0.1,requests==2.31.0,rich==13.7.0,selinux==0.2.1,six==1.16.0,subprocess-tee==0.3.5,text-unidecode==1.3,typing_extensions==4.7.1,urllib3==2.0.7,zipp==3.15.0
py37-ansible30 run-test-pre: PYTHONHASHSEED='1669044436'
py37-ansible30 run-test: commands[0] | molecule test -s default --destroy always
INFO     default scenario test matrix: destroy, create, converge, destroy
INFO     Performing prerun...
INFO     Set ANSIBLE_LIBRARY=/root/.cache/ansible-compat/b984a4/modules:/root/.ansible/plugins/modules:/usr/share/ansible/plugins/modules
INFO     Set ANSIBLE_COLLECTIONS_PATH=/root/.cache/ansible-compat/b984a4/collections:/root/.ansible/collections:/usr/share/ansible/collections
INFO     Set ANSIBLE_ROLES_PATH=/root/.cache/ansible-compat/b984a4/roles:/root/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles
ERROR    Computed fully qualified role name of vector_role does not follow current galaxy requirements.
Please edit meta/main.yml and assure we can correctly determine full role name:

galaxy_info:
role_name: my_name  # if absent directory name hosting role is used instead
namespace: my_galaxy_namespace  # if absent, author is used instead

Namespace: https://galaxy.ansible.com/docs/contributing/namespaces.html#galaxy-namespace-limitations
Role: https://galaxy.ansible.com/docs/contributing/creating_role.html#role-names

As an alternative, you can add 'role-name' to either skip_list or warn_list.

Traceback (most recent call last):
  File "/opt/vector-role/.tox/py37-ansible30/bin/molecule", line 8, in <module>
    sys.exit(main())
  File "/opt/vector-role/.tox/py37-ansible30/lib/python3.7/site-packages/click/core.py", line 1157, in __call__
    return self.main(*args, **kwargs)
  File "/opt/vector-role/.tox/py37-ansible30/lib/python3.7/site-packages/click/core.py", line 1078, in main
    rv = self.invoke(ctx)
  File "/opt/vector-role/.tox/py37-ansible30/lib/python3.7/site-packages/click/core.py", line 1688, in invoke
    return _process_result(sub_ctx.command.invoke(sub_ctx))
  File "/opt/vector-role/.tox/py37-ansible30/lib/python3.7/site-packages/click/core.py", line 1434, in invoke
    return ctx.invoke(self.callback, **ctx.params)
  File "/opt/vector-role/.tox/py37-ansible30/lib/python3.7/site-packages/click/core.py", line 783, in invoke
    return __callback(*args, **kwargs)
  File "/opt/vector-role/.tox/py37-ansible30/lib/python3.7/site-packages/click/decorators.py", line 33, in new_func
    return f(get_current_context(), *args, **kwargs)
  File "/opt/vector-role/.tox/py37-ansible30/lib/python3.7/site-packages/molecule/command/test.py", line 161, in test
    base.execute_cmdline_scenarios(scenario_name, args, command_args, ansible_args)
  File "/opt/vector-role/.tox/py37-ansible30/lib/python3.7/site-packages/molecule/command/base.py", line 111, in execute_cmdline_scenarios
    scenario.config.runtime.prepare_environment(install_local=True)
  File "/opt/vector-role/.tox/py37-ansible30/lib/python3.7/site-packages/ansible_compat/runtime.py", line 334, in prepare_environment
    self._install_galaxy_role(self.project_dir, ignore_errors=True)
  File "/opt/vector-role/.tox/py37-ansible30/lib/python3.7/site-packages/ansible_compat/runtime.py", line 478, in _install_galaxy_role
    raise InvalidPrerequisiteError(msg)
ansible_compat.errors.InvalidPrerequisiteError: Computed fully qualified role name of vector_role does not follow current galaxy requirements.
Please edit meta/main.yml and assure we can correctly determine full role name:

galaxy_info:
role_name: my_name  # if absent directory name hosting role is used instead
namespace: my_galaxy_namespace  # if absent, author is used instead

Namespace: https://galaxy.ansible.com/docs/contributing/namespaces.html#galaxy-namespace-limitations
Role: https://galaxy.ansible.com/docs/contributing/creating_role.html#role-names

As an alternative, you can add 'role-name' to either skip_list or warn_list.

ERROR: InvocationError for command /opt/vector-role/.tox/py37-ansible30/bin/molecule test -s default --destroy always (exited with code 1)
py39-ansible210 installed: ansible==2.10.7,ansible-base==2.10.17,ansible-compat==4.1.11,ansible-core==2.15.8,attrs==23.2.0,bracex==2.4,cffi==1.16.0,click==8.1.7,click-help-colors==0.9.4,cryptography==42.0.0,distro==1.9.0,enrich==1.2.7,importlib-resources==5.0.7,Jinja2==3.1.3,jmespath==1.0.1,jsonschema==4.21.1,jsonschema-specifications==2023.12.1,lxml==5.1.0,markdown-it-py==3.0.0,MarkupSafe==2.1.4,mdurl==0.1.2,molecule==6.0.3,molecule-podman==2.0.3,packaging==23.2,pluggy==1.3.0,pycparser==2.21,Pygments==2.17.2,PyYAML==6.0.1,referencing==0.32.1,resolvelib==1.0.1,rich==13.7.0,rpds-py==0.17.1,selinux==0.3.0,subprocess-tee==0.4.1,typing_extensions==4.9.0,wcmatch==8.5
py39-ansible210 run-test-pre: PYTHONHASHSEED='1669044436'
py39-ansible210 run-test: commands[0] | molecule test -s default --destroy always
WARNING  Driver podman does not provide a schema.
INFO     default scenario test matrix: destroy, create, converge, destroy
INFO     Performing prerun with role_name_check=1...
WARNING  Computed fully qualified role name of vector_role does not follow current galaxy requirements.
Please edit meta/main.yml and assure we can correctly determine full role name:

galaxy_info:
role_name: my_name  # if absent directory name hosting role is used instead
namespace: my_galaxy_namespace  # if absent, author is used instead

Namespace: https://galaxy.ansible.com/docs/contributing/namespaces.html#galaxy-namespace-limitations
Role: https://galaxy.ansible.com/docs/contributing/creating_role.html#role-names

As an alternative, you can add 'role-name' to either skip_list or warn_list.

ERROR    CompletedProcess(args=['ansible-galaxy', 'collection', 'list', '--format=json'], returncode=250, stdout='the full traceback was:\n\nTraceback (most recent call last):\n  File "/opt/vector-role/.tox/py39-ansible210/bin/ansible-galaxy", line 92, in <module>\n    mycli = getattr(__import__("ansible.cli.%s" % sub, fromlist=), myclass)\n  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/ansible/cli/galaxy.py", line 24, in <module>\n    from ansible.galaxy.collection import (\n  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/ansible/galaxy/collection/__init__.py", line 90, in <module>\n    from ansible.galaxy.collection.concrete_artifact_manager import (\n  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/ansible/galaxy/collection/concrete_artifact_manager.py", line 30, in <module>\n    from ansible.galaxy.api import should_retry_error\nImportError: cannot import name \'should_retry_error\' from \'ansible.galaxy.api\' (/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/ansible/galaxy/api.py)\n', stderr="ERROR! Unexpected Exception, this is probably a bug: cannot import name 'should_retry_error' from 'ansible.galaxy.api' (/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/ansible/galaxy/api.py)\n")
Traceback (most recent call last):
  File "/opt/vector-role/.tox/py39-ansible210/bin/molecule", line 8, in <module>
    sys.exit(main())
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/click/core.py", line 1157, in __call__
    return self.main(*args, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/click/core.py", line 1078, in main
    rv = self.invoke(ctx)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/click/core.py", line 1688, in invoke
    return _process_result(sub_ctx.command.invoke(sub_ctx))
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/click/core.py", line 1434, in invoke
    return ctx.invoke(self.callback, **ctx.params)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/click/core.py", line 783, in invoke
    return __callback(*args, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/click/decorators.py", line 33, in new_func
    return f(get_current_context(), *args, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/molecule/command/test.py", line 113, in test
    base.execute_cmdline_scenarios(scenario_name, args, command_args, ansible_args)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/molecule/command/base.py", line 113, in execute_cmdline_scenarios
    scenario.config.runtime.prepare_environment(
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/ansible_compat/runtime.py", line 684, in prepare_environment
    self.load_collections()
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/ansible_compat/runtime.py", line 285, in load_collections
    raise RuntimeError(msg)
RuntimeError: Unable to list collections: CompletedProcess(args=['ansible-galaxy', 'collection', 'list', '--format=json'], returncode=250, stdout='the full traceback was:\n\nTraceback (most recent call last):\n  File "/opt/vector-role/.tox/py39-ansible210/bin/ansible-galaxy", line 92, in <module>\n    mycli = getattr(__import__("ansible.cli.%s" % sub, fromlist=[myclass]), myclass)\n  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/ansible/cli/galaxy.py", line 24, in <module>\n    from ansible.galaxy.collection import (\n  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/ansible/galaxy/collection/__init__.py", line 90, in <module>\n    from ansible.galaxy.collection.concrete_artifact_manager import (\n  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/ansible/galaxy/collection/concrete_artifact_manager.py", line 30, in <module>\n    from ansible.galaxy.api import should_retry_error\nImportError: cannot import name \'should_retry_error\' from \'ansible.galaxy.api\' (/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/ansible/galaxy/api.py)\n', stderr="ERROR! Unexpected Exception, this is probably a bug: cannot import name 'should_retry_error' from 'ansible.galaxy.api' (/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/ansible/galaxy/api.py)\n")
ERROR: InvocationError for command /opt/vector-role/.tox/py39-ansible210/bin/molecule test -s default --destroy always (exited with code 1)
py39-ansible30 installed: ansible==3.0.0,ansible-base==2.10.17,ansible-compat==4.1.11,ansible-core==2.15.8,attrs==23.2.0,bracex==2.4,cffi==1.16.0,click==8.1.7,click-help-colors==0.9.4,cryptography==42.0.0,distro==1.9.0,enrich==1.2.7,importlib-resources==5.0.7,Jinja2==3.1.3,jmespath==1.0.1,jsonschema==4.21.1,jsonschema-specifications==2023.12.1,lxml==5.1.0,markdown-it-py==3.0.0,MarkupSafe==2.1.4,mdurl==0.1.2,molecule==6.0.3,molecule-podman==2.0.3,packaging==23.2,pluggy==1.3.0,pycparser==2.21,Pygments==2.17.2,PyYAML==6.0.1,referencing==0.32.1,resolvelib==1.0.1,rich==13.7.0,rpds-py==0.17.1,selinux==0.3.0,subprocess-tee==0.4.1,typing_extensions==4.9.0,wcmatch==8.5
py39-ansible30 run-test-pre: PYTHONHASHSEED='1669044436'
py39-ansible30 run-test: commands[0] | molecule test -s default --destroy always
WARNING  Driver podman does not provide a schema.
INFO     default scenario test matrix: destroy, create, converge, destroy
INFO     Performing prerun with role_name_check=1...
WARNING  Computed fully qualified role name of vector_role does not follow current galaxy requirements.
Please edit meta/main.yml and assure we can correctly determine full role name:

galaxy_info:
role_name: my_name  # if absent directory name hosting role is used instead
namespace: my_galaxy_namespace  # if absent, author is used instead

Namespace: https://galaxy.ansible.com/docs/contributing/namespaces.html#galaxy-namespace-limitations
Role: https://galaxy.ansible.com/docs/contributing/creating_role.html#role-names

As an alternative, you can add 'role-name' to either skip_list or warn_list.

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
ERROR: InvocationError for command /opt/vector-role/.tox/py39-ansible30/bin/molecule test -s default --destroy always (exited with code 1)
_______________________________________________________________________ summary ________________________________________________________________________
ERROR:   py37-ansible210: commands failed
ERROR:   py37-ansible30: commands failed
ERROR:   py39-ansible210: commands failed
ERROR:   py39-ansible30: commands failed

</details> 

7. Добавьте новый тег на коммит с рабочим сценарием в соответствии с семантическим версионированием.

После выполнения у вас должно получится два сценария molecule и один tox.ini файл в репозитории. Не забудьте указать в ответе теги решений Tox и Molecule заданий. В качестве решения пришлите ссылку на ваш репозиторий и скриншоты этапов выполнения задания.

Исправления вносил в существующий default сценарий. 

[Release 1.1.0](https://github.com/SSitkarev/vector_role/tree/1.1.0)