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

When the server is started the very first time, you'll encounter a warning message about EULA:

    [23:06:52] [ServerMain/WARN]: Failed to load eula.txt
    [23:06:52] [ServerMain/INFO]: You need to agree to the EULA in order to run the server. Go to eula.txt for more info.

Open the configuration file at `<mcj_install_dir>/workspace/server.properties`:

    #By changing the setting below to TRUE you are indicating your agreement to our EULA (https://aka.ms/MinecraftEULA).
    #Sat Feb 15 23:06:52 UTC 2025
    eula=false

and then replace `eula=false` with `eula=true`.
