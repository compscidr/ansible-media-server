# sonarr
see: https://docs.linuxserver.io/images/docker-sonarr/

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
        - role: compscidr.media_server.sonarr
```

# Variables
Variable                                | Description
--------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
sonarr_folder                           | sonarr config folder
sonarr_tv_folder                        | where the completed tv shows will be moved to
sonarr_transmissions_downloads_folder    | transmission download folder
sonarr_sabnzbd_downloads_folder:         | sabznbd downlod folder
sonarr_port                             | the port where sonarr will listen on
sonarr_tz                               | sonarr timezone
sonarr_pid                              | the user id for volume permissions
sonarr_gid                              | the group id for volume permissions