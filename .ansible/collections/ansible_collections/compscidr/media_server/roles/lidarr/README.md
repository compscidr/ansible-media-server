# lidarr
see: https://docs.linuxserver.io/images/docker-lidarr

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
        - role: compscidr.media_server.lidarr
```

# Variables
Variable                                | Description
--------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
lidarr_folder                           | lidarr config folder
lidarr_music_folder                     | where the completed music should be moved to
lidarr_transmission_downloads_folder    | transmission download folder
lidarr_sabnzbd_downoads_folder          | sabnzbd download folder
lidarr_port                             | the port lidarr will listen on
lidarr_tz                               | lidarr timezone
lidarr_pid                              | the user id for volume permissions
lidarr_gid                              | the group id for volume permissions