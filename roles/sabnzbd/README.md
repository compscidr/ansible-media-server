# sabnzbd
see: https://docs.linuxserver.io/images/docker-sabnzbd/

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
        - role: compscidr.media_server.sabnzbd
```

# Variables
Variable                                | Description
--------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
install_docker                          | Set to true to install docker with the nickjj.docker role (defaults to false)
sabnzbd_folder                          | config folder
sabnzbd_download_folder                 | sabnzbd download folder
sabnzbd_port                            | port sabnzbd will listen on
sabnzbd_tz                              | sabnzbd timezone
sabnzbd_pid                             | the user id for volume permission
sabnzbd_gid                             | the group id for volume permission