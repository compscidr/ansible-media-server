# soularr Role

This role installs and configures the [soularr](https://github.com/mrusse/soularr) container - a tool that integrates slskd with Lidarr for automated music downloads.

## Purpose

soularr monitors Lidarr's wanted list and automatically searches slskd (Soulseek) for missing albums/tracks. It bridges the gap between Lidarr's music management and Soulseek's peer-to-peer sharing network.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
# Docker installation control
soularr_install_docker: false

# soularr configuration
soularr_folder: /etc/soularr
soularr_downloads_folder: "{{ media_storage_base_path }}/downloads/complete/music"
soularr_memory: "1g"
soularr_memory_swap: "1g"

# Docker network (use custom network for container name resolution)
soularr_networks: []
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
    - compscidr.media_server.slskd    # Required - provides slskd
    - compscidr.media_server.lidarr   # Required - provides Lidarr
    - compscidr.media_server.soularr  # Bridges slskd and Lidarr
```

## Post-Installation

After deployment, configure soularr by editing the config file in `{{ soularr_folder }}/data/`:
1. Set your Lidarr API key and URL
2. Set your slskd API key and URL
3. Configure search preferences

## License

GPLv3

## Author Information

Jason Ernst
