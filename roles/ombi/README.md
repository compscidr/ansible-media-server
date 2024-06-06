# ombi
see: https://docs.linuxserver.io/images/docker-ombi/

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
        - role: compscidr.media_server.ombi
```

# Variables
Variable                                | Description
--------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
install_docker                          | Set to true to install docker with the nickjj.docker role (defaults to false)
ombi_port                               | The port ombi will listen on
ombi_tz                                 | The timezone to use for ombi
ombi_folder                             | The config folder for ombi
ombi_gid                                | the user id for volume permissions
ombi_pid                                | the group id for volume permissions
ombi_virtual_host                       | the host if ombi is behind a nginx reverse proxy
ombi_virtual_port                       | the port ombi is listening on behind the nginx proxy
ombi_letsencrypt_host                   | the hostname to obtain letsencrypt certificates for
ombi_letsencrypt_email                  | the email address associated with the letsencrypt certs