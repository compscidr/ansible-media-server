# Flaresolverr
See: https://github.com/FlareSolverr/FlareSolverr

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
        - role: compscidr.media_server.flaresolverr
```

# Variables
Variable                                | Description
--------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
role (defaults to false)
flare_port                              | The port flaresolverr will listen on
flare_captcha_solver                    | The captcha solver used for flaresolverr
flare_tz                                | The timezone to use for flaresolverr