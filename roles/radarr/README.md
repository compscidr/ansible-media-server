# radarr
see: https://docs.linuxserver.io/images/docker-radarr

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
        - role: compscidr.media_server.radarr
```

# Variables
Variable                                | Description
--------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
radarr_folder                           | radarr config folder
radarr_movies_folder                    | where the completed moves should be moved to
radarr_transmission_downloads_folder    | transmission download folder
radarr_sabnzbd_downloads_folder          | sabnzbd download folder
radarr_port                             | the port raddarr will listen on
radarr_tz                               | radarr timezone
radarr_pid                              | the user id for volume permissions
radarr_gid                              | the group id for volume permissions