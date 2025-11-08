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
        mcj_install_id: minecraft-java
        mcj_os_user: minecraft
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
            mcj_install_id: minecraft-java
            mcj_os_user: minecraft
            mcj_java_opts: -Xmx2048M - Xms1024M
            mcj_eula_accepted: true
            mcj_server_properties:
              motd: "A Minecraft Server managed by Ansible Role Minecraft Java"

On machines with systemd, a `<mcj_install_id>` service will be provisioned so you can use systemctl to manage the server.

    sudo systemctl start <mcj_install_id>.service
    sudo systemctl stop <mcj_install_id>.service
    sudo systemctl status <mcj_install_id>.service

    alias <mcj_install_id>-conf='vi <mcj_install_dir>/workspace/server.properties'
    alias <mcj_install_id>-log='tail -f <mcj_install_dir>/workspace/logs/latest.log'

Config
------

| Variable | Description | Default | Example |
|----------|-------------|---------|---------|
| mcj_minecraft_version | [Supported Minecraft version number](https://github.com/littlegodzillalaboratory/ansible-role-minecraft-java/blob/main/vars/main.yml#L2) | `1.21` |  `1.21.10` |
| mcj_install_id | Minecraft installation ID, useful to distinguish multiple installations on the same machine | `minecraft-java` | `minecraft-1` |
| mcj_install_dir | Minecraft installation directory | `/opt/minecraft` | `/some/other/path` |
| mcj_os_user | System user which the Java process runs under | `minecraft` | `someuser` |
| mcj_env_path | To be used as the [environment PATH](https://en.wikipedia.org/wiki/PATH_(variable)) which the Minecraft server runs with. Must have `java` command under one of the path values. | `/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin` | `/home/someuser/.sdkman/candidates/java/current/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin` |
| mcj_java_opts | Server [Java options](https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/jvm-options-java-parameters-command-line-environment-variable-list-xms-xmx-memory) | `-Xmx2048M -Xms1024M` | `-Xmx2048M -Xms1024M` |
| mcj_eula_accepted | Accept the Minecraft [EULA](https://nodecraft.com/support/games/minecraft/general/minecraft-eula) when set to true | `true` | `false` |
| mcj_server_properties | Minecraft [server properties](https://minecraft.fandom.com/wiki/Server.properties) key-value pairs. | `motd: "A Minecraft Server managed by Ansible Role Minecraft Java"` | `difficulty: normal`<br/>`gamemode: survival`<br/>`hardcore: "false"` |
