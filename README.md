# ansible-media-server
[![Static Badge](https://img.shields.io/badge/Ansible_galaxy-Download-blue)](https://galaxy.ansible.com/ui/repo/published/compscidr/media_server/)
[![ansible lint](https://github.com/compscidr/ansible-media-server/actions/workflows/check.yml/badge.svg)](https://github.com/compscidr/ansible-media-server/actions/workflows/check.yml)
[![ansible lint rules](https://img.shields.io/badge/Ansible--lint-rules%20table-blue.svg)](https://ansible.readthedocs.io/projects/lint/rules/)

A collection of roles for running a media server with docker containers:
- flaresolverr
- jackett
- ombi
- plex
- prowlarr
- radarr
- sabnzbd
- sonarr
- transmission

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
    - role: compscidr.media_server.transmission
    - role: compscidr.media_server.plex
      vars:
        plex_dri_devices: true
        plex_bonjour_port: 5354
    - role: compscidr.media_server.flaresolverr
    - role: compscidr.media_server.jackett
    - role: compscidr.media_server.sonarr
    - role: compscidr.media_server.radarr
    - role: compscidr.media_server.prowlarr
    - role: compscidr.media_server.sabnzbd
```

# Variables
Variable                                | Description
--------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
install_docker                          | Set to true to install docker with the nickjj.docker role (defaults to false)
flare_port                              | The port flaresolverr will listen on
flare_captcha_solver                    | The captcha solver used for flaresolverr
flare_tz                                | The timezone to use for flaresolverr
jackett_folder                          | The config folder for jacket
jackett_download_folder                 | The downloads folder for jackett
jackett_port                            | The port jackett will listen on
jackett_tz                              | The timezone to use for jackett
jackett_pid                             | the user id for volume permissions
jackett_gid                             | the group id for volume permissions
ombi_port                               | The port ombi will listen on
ombi_tz                                 | The timezone to use for ombi
ombi_folder                             | The config folder for ombi
ombi_gid                                | the user id for volume permissions
ombi_pid                                | the group id for volume permissions
ombi_virtual_host                       | the host if ombi is behind a nginx reverse proxy
ombi_virtual_port                       | the port ombi is listening on behind the nginx proxy
ombi_letsencrypt_host                   | the hostname to obtain letsencrypt certificates for
ombi_letsencrypt_email                  | the email address associated with the letsencrypt certs
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
prowlarr_port                           | The port prowlarr will listen on
prowlarr_folder                         | prowlarr config folder
prowlarr_tz                             | prowlarr timzeone
prowlarr_pid                            | the user id for volume permissions
prowlarr_gid                            | the group id for volume permissions
radarr_folder                           | radarr config folder
radarr_movies_folder                    | where the completed moves should be moved to
radarr_transmission_downloads_folder    | transmission download folder
radarr_sabnzbd_downoads_folder          | sabnzbd download folder
radarr_port                             | the port raddarr will listen on
radarr_tz                               | radarr timezone
radarr_pid                              | the user id for volume permissions
radarr_gid                              | the group id for volume permissions
sabnzbd_folder                          | config folder
sabnzbd_download_folder                 | sabnzbd download folder
sabnzbd_port                            | port sabnzbd will listen on
sabnzbd_tz                              | sabnzbd timezone
sabnzbd_pid                             | the user id for volume permission
sabnzbd_gid                             | the group id for volume permission
sonarr_folder                           | sonarr config folder
sonarr_tv_folder                        | where the completed tv shows will be moved to
sonarr_tranmissions_downloads_folder    | transmission download folder
sonarr_sabnzbd_downoads_folder:         | sabznbd downlod folder
sonarr_port                             | the port where sonarr will listen on
sonarr_tz                               | sonarr timezone
sonarr_pid                              | the user id for volume permissions
sonarr_gid                              | the group id for volume permissions
transmission_port                       | port transmission will listen on
transmission_folder                     | transmission config folder
transmission_downloads_folder           | tranmission download folder
transmission_pid                        | the user id for volume permissions
transmission_gid                        | the group id for volume permissions
transmission_tz                         | transmission timezone
transmission_env_file: "{{ transmission_folder }}/.env" | the environment file which contains env variables for things like VPN login credentials, see https://github.com/haugene/docker-transmission-openvpn

