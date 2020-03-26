 Ansible установка zabbix-agent v4.4 на ubuntu
# Подготовка...
Устанавливаем, обновляем пакеты ansible. Т.к в большинстве репозитариев Unix OS версия ansible достаточно старая, устанавливал/обновлял с помощью pip

apt install python-pip
pip install ansible -U

Текущая версия:
ansible --version = ansible 2.9.6

## Zabbix пакеты репозитория качаются с оф. сайта repo.zabbix.com, согласно рекомендациям...
https://www.zabbix.com/documentation/current/ru/manual/installation/install_from_packages/debian_ubuntu

Если нужно поправить только файл конфигурации, дотасточно закомментировать -include: pkg.yaml в файле ./zabbix-agent/tasks/main.yml

"├── roles"
"│   └── zabbix-agent"
│       ├── handlers
│       │   └── main.yml
│       └── tasks
│           ├── configure.yaml
│           ├── main.yml
│           └── pkg.yaml

Переменные Server и SeerverActive устанавливаются в файле zabbix-agent-playbook.yaml

    zabbix_agent_server: 192.168.33.30
    zabbix_agent_serveractive: 192.168.33.30

Что касается переменной Hostname, вероятно её значение необходимо брать из фактов собираемых на конкретном хосте. Но у меня нет точной информации каким образом оно формируется. 
Поэтому я вынес переменную в файл ./hosts, если переменная указана для хоста, то ее значение будет подствляться в файл конфигурации.

Тестировал роль на OS: Ubuntu 16.04 + Ubuntu 18.04
