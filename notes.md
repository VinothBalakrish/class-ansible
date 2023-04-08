devops@ip-172-31-28-86:~$ ls /etc/ansible/
ansible.cfg  hosts  roles
devops@ip-172-31-28-86:~$ vi inventory
devops@ip-172-31-28-86:~$ ansible -m ping -i inventory all 
52.91.96.69 | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: devops@52.91.96.69: Permission denied (publickey,password).",
    "unreachable": true
}
devops@ip-172-31-28-86:~$ ansible -m ping -i inventory all --ask-pass
SSH password: 
52.91.96.69 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}


devops@ip-172-31-28-86:~$ ansible -i inventory all -m command -a "touch a.txt /tmp" --ask-pass
SSH password: 
52.91.96.69 | CHANGED | rc=0 >>

devops@ip-172-31-28-86:~$ ansible -i inventory all -m command -a "ls /tmp" --ask-pass
SSH password: 
52.91.96.69 | CHANGED | rc=0 >>
ansible_ansible.legacy.command_payload_ypscb7h7
snap-private-tmp
systemd-private-b49ab0b7b1ed4058843645a29a283a76-chrony.service-S3pNwD
systemd-private-b49ab0b7b1ed4058843645a29a283a76-systemd-logind.service-2Fyo5T
systemd-private-b49ab0b7b1ed4058843645a29a283a76-systemd-resolved.service-cXAMJo
devops@ip-172-31-28-86:~$ ansible -i inventory all -m user -a "name=soundar" --ask-pass
SSH password: 
52.91.96.69 | FAILED! => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "msg": "useradd: Permission denied.\nuseradd: cannot lock /etc/passwd; try again later.\n",
    "name": "soundar",
    "rc": 1
}
devops@ip-172-31-28-86:~$ ansible -i inventory all -m user -a "name=soundar" --ask-pass --become
SSH password: 
52.91.96.69 | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": true,
    "comment": "",
    "create_home": true,
    "group": 1002,
    "home": "/home/soundar",
    "name": "soundar",
    "shell": "/bin/sh",
    "state": "present",
    "system": false,
    "uid": 1002
}
