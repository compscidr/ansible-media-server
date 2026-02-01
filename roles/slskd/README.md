# slskd Role

This role installs and configures the [slskd](https://github.com/slskd/slskd) container - a modern Soulseek client with a web interface.

## Purpose

slskd provides access to the Soulseek peer-to-peer music sharing network through a web-based interface. Combined with soularr, it can automate music downloads for Lidarr.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
# Docker installation control
slskd_install_docker: false

# slskd configuration
slskd_folder: /etc/slskd
slskd_music_folder: "{{ media_storage_base_path }}/music"
slskd_downloads_folder: "{{ media_storage_base_path }}/downloads/complete/music"
slskd_incomplete_folder: "{{ media_storage_base_path }}/downloads/incomplete"
slskd_port: 5030
slskd_https_port: 5031
slskd_soulseek_port: 50300
slskd_tz: "America/Los_Angeles"
slskd_memory: "1g"
slskd_memory_swap: "1g"

# Docker network (use custom network for container name resolution)
slskd_networks: []
```

## Dependencies

- `media_storage` - Creates storage directories and provides UID/GID detection

## Example Playbook

```yaml
- hosts: media_servers
  vars:
    media_user_user: myuser
    media_user_group: mygroup
    media_storage_base_path: /storage
  roles:
    - compscidr.media_server.slskd
```

## Ports

- **5030**: Web UI (HTTP)
- **5031**: Web UI (HTTPS)
- **50300**: Soulseek listening port

## Post-Installation

After deployment, access the web UI at `http://host:5030` to:
1. Configure your Soulseek credentials
2. Set up sharing preferences
3. Configure download settings

## License

GPLv3

## Author Information

Jason Ernst
