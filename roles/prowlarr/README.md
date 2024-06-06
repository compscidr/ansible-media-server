# prowlarr
see: https://docs.linuxserver.io/images/docker-prowlarr/

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
        - role: compscidr.media_server.prowlarr
```

# Variables
Variable                                | Description
--------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
install_docker                          | Set to true to install docker with the nickjj.docker role (defaults to false)
prowlarr_port                           | The port prowlarr will listen on
prowlarr_folder                         | prowlarr config folder
prowlarr_tz                             | prowlarr timzeone
prowlarr_pid                            | the user id for volume permissions
prowlarr_gid                            | the group id for volume permissions