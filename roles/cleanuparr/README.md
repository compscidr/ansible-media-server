# cleanuparr Role

This role installs and configures the [Cleanuparr](https://github.com/Cleanuparr/Cleanuparr) container - a download manager for the *arr ecosystem that removes and blocks stalled, failed-import and malicious downloads, and cleans up orphaned files.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
# Docker installation control
cleanuparr_install_docker: false

# Cleanuparr configuration
cleanuparr_folder: /etc/cleanuparr
cleanuparr_downloads_folder: "{{ media_storage_base_path }}/downloads"
cleanuparr_port: 11011
cleanuparr_tz: "America/Los_Angeles"
cleanuparr_memory: "1g"
cleanuparr_memory_swap: "1g"

# Docker network (use custom network for container name resolution)
cleanuparr_networks: []

# Extra bind mounts appended to the container's volumes
cleanuparr_extra_volumes: []
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
    - compscidr.media_server.sonarr
    - compscidr.media_server.radarr
    - compscidr.media_server.transmission
    - compscidr.media_server.cleanuparr
```

## Post-Installation

1. Open the web UI on port `cleanuparr_port` (default 11011) and set an account under `Settings → Account`; there is no auth until you do.
2. In Prowlarr, enable `Sync Reject Blocklisted Torrent Hashes While Grabbing` on each app (or the equivalent per-indexer option in each *arr) so blocked releases do not come back.
3. Add your *arrs and download clients by container name (e.g. `http://sonarr:8989`, `http://transmission:9091`) when running on the shared media network.

## License

GPLv3

## Author Information

Jason Ernst
