# jackett
see: https://docs.linuxserver.io/images/docker-jackett/

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
        - role: compscidr.media_server.jackett
```

# Variables
Variable                                | Description
--------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
jackett_folder                          | The config folder for jacket
jackett_download_folder                 | The downloads folder for jackett
jackett_port                            | The port jackett will listen on
jackett_tz                              | The timezone to use for jackett
jackett_pid                             | the user id for volume permissions
jackett_gid                             | the group id for volume permissions