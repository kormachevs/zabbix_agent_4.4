 Ansible установка zabbix-agent v4.4 на ubuntu
# Подготовка...
Устанавливаем, обновляем пакеты ansible(на управляющем хосте). Т.к в большинстве репозитариев Unix OS версия ansible достаточно старая, устанавливал/обновлял с помощью pip

apt install python-pip

pip install ansible -U

Текущая версия:
ansible --version = ansible 2.9.6

## Zabbix пакеты репозитория качаются с оф. сайта repo.zabbix.com, согласно рекомендациям...
https://www.zabbix.com/documentation/current/ru/manual/installation/install_from_packages/debian_ubuntu

Если нужно поправить только файл конфигурации, дотасточно передать значение False переменной zabbix_agent_install_agent или поправить в playbook-е:

    zabbix_agent_install_agent: False

Переменные Server и SeerverActive устанавливаются в файле zabbix-agent-playbook.yaml

    zabbix_agent_server: 192.168.33.30
    zabbix_agent_serveractive: 192.168.33.30

Hostname = ansible_hostname

Запуск плейбука:
 
    ansible-playbook zabbix-agent-playbook.yaml


Тестировал роль на OS: Ubuntu 16.04 + Ubuntu 18.04
