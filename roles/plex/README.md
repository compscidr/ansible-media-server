# plex
see: https://docs.linuxserver.io/images/docker-plex/

## Usage
add the collection to your meta/requirements.yml:
```
collections:
    - name: compscidr.media_server
        version: "<insert version here>"
```

Install the collection:
```
ansible-galaxy install -r meta/requirements.yml
```

Use in a playbook:
```
---
- name: Media Services
    hosts: all
    vars_files:
        - vars/some_vars.yml
    roles:
        - role: compscidr.media_server.plex
```

# Variables
Variable                                | Description
--------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
plex_port                               | The port plex will listen on
plex_dlna_port                          | The port plex will listen on for DNLA requests (udp)
plex_bonjour_port                       | The port plex will listen on for bounjour/avahi protocol
plex_roku_port                          | The port plex will listen on for roku companion
plex_gdm_port1                          | The port plex will listen on for GDM network discovery https://support.plex.tv/articles/201543147-what-network-ports-do-i-need-to-allow-through-my-firewall/
plex_gdm_port2                          | The port plex will listen on for GDM network discovery https://support.plex.tv/articles/201543147-what-network-ports-do-i-need-to-allow-through-my-firewall/
plex_gdm_port3                          | The port plex will listen on for GDM network discovery https://support.plex.tv/articles/201543147-what-network-ports-do-i-need-to-allow-through-my-firewall/
plex_gdm_port4                          | The port plex will listen on for GDM network discovery https://support.plex.tv/articles/201543147-what-network-ports-do-i-need-to-allow-through-my-firewall/
plex_dlna_server_port                   | The port plex will listen on for DNLA requests (tcp)
plex_folder                             | plex config folder
plex_tv_folder                          | where plex tv shows are located
plex_movies_folder                      | where plex movies are located
plex_tz                                 | plex timezome
plex_pid                                | the user id for volume permissions
plex_gid                                | the group id for volume permissions
plex_dvb_devices                        | DVB transcoding acceleration
plex_dri_devices                        | DRI transcoding acceleration
plex_claim                              | Used to attach a plex token to the server, see: https://docs.linuxserver.io/images/docker-plex/#environment-variables-e. This only needs to be present during initial setup as long as the storage volume hasn't been clobbered