# transmision
see: https://github.com/haugene/docker-transmission-openvpn

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
install_docker                          | Set to true to install docker with the nickjj.docker role (defaults to false)
transmission_port                       | port transmission will listen on
transmission_folder                     | transmission config folder
transmission_downloads_folder           | tranmission download folder
transmission_pid                        | the user id for volume permissions
transmission_gid                        | the group id for volume permissions
transmission_tz                         | transmission timezone
transmission_env_file: "{{ transmission_folder }}/.env" | the environment file which contains env variables for things like VPN login credentials, see https://github.com/haugene/docker-transmission-openvpn

## VPN usage:
Note: if you're planning on using the VPN, you must setup the ENV variables via an .env file that
is moved into {{ transmission_env_file }} prior to the deploy transmission test.

For example, something like this:
```
- name: Create Transmission Directories
    tags: transmission
    become: true
    ansible.builtin.file:
        path: "/etc/transmission/"
        state: directory
        mode: '755'
        owner: root
        group: root

- name: Set transmission nordvpn credentials
    tags: transmission
    become: true
    copy:
        mode: '755'
        owner: root
        group: root
        dest: "/etc/transmission/.env"
        content: |
            TRANSMISSION_WEB_UI=transmission-web-control
            OPENVPN_PROVIDER=NORDVPN
            NORDVPN_PROTOCOL=udp
            OPENVPN_USERNAME={{ nordvpn_user }}
            OPENVPN_PASSWORD={{ nordvpn_password }}
            NORDVPN_COUNTRY:=US
            NORDVPN_CATEGORY=P2P
            LOCAL_NETWORK=10.0.0.0/24
            HEALTH_CHECK_HOST=8.8.8.8
```