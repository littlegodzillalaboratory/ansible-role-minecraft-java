<img align="right" src="https://raw.github.com/littlegodzillalaboratory/ansible-role-minecraft-java/main/avatar.jpg" alt="Avatar"/>

[![Build Status](https://github.com/littlegodzillalaboratory/ansible-role-minecraft-java/workflows/CI/badge.svg)](https://github.com/littlegodzillalaboratory/ansible-role-minecraft-java/actions?query=workflow%3ACI)
[![Security Status](https://snyk.io/test/github/littlegodzillalaboratory/ansible-role-minecraft-java/badge.svg)](https://snyk.io/test/github/littlegodzillalaboratory/ansible-role-minecraft-java)

Ansible Role Minecraft Java
---------------------------

Ansible role for provisioning [Minecraft Java edition](https://www.minecraft.net/en-us/store/minecraft-java-bedrock-edition-pc) on Linux machine.

Usage
-----

Add the role to playbook:

    - hosts: all

      vars:
        mcj_minecraft_version: '1.21'
        mcj_install_dir: /opt/minecraft
        mcj_id: minecraft-java
        mcj_user: minecraft
        mcj_java_opts: -Xmx2048M - Xms1024M
        mcj_eula_accepted: true
        mcj_server_properties:
          motd: "A Minecraft Server managed by Ansible Role Minecraft Java"
          
      roles:
        - littlegodzillalaboratory.minecraft-java

Or alternatively, as a task using import role:

      tasks:

        - ansible.builtin.import_role:
            name: littlegodzillalaboratory.minecraft-java
          vars:
            mcj_minecraft_version: '1.21'
            mcj_install_dir: /opt/minecraft
            mcj_id: minecraft-java
            mcj_user: minecraft
            mcj_java_opts: -Xmx2048M - Xms1024M
            mcj_eula_accepted: true
            mcj_server_properties:
              motd: "A Minecraft Server managed by Ansible Role Minecraft Java"

On machines with systemd, a `<mcj_id>` service will be provisioned so you can use systemctl to manage the server.

    sudo systemctl start <mcj_id>.service
    sudo systemctl stop <mcj_id>.service
    sudo systemctl status <mcj_id>.service

    alias <mcj_id>-conf='vi <mcj_install_dir>/workspace/server.properties'
    alias <mcj_id>-log='tail -f <mcj_install_dir>/workspace/logs/latest.log'

Config
------

