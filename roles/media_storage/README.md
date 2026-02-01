# Media Storage Role

This role creates and manages shared media storage directories for all media server components (Plex, Sonarr, Radarr, Lidarr, Transmission, SABnzbd, etc.).

## Purpose

The `media_storage` role creates shared media storage directories. It depends on the `media_user` role for UID/GID detection, ensuring:
- Consistent user/group ownership across all media directories
- Automatic creation of required media directories
- Single point of configuration for storage paths

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
# Base path for all media storage
media_storage_base_path: /storage

# List of directories to create
media_storage_directories:
  - "{{ media_storage_base_path }}"
  - "{{ media_storage_base_path }}/downloads"
  - "{{ media_storage_base_path }}/downloads/complete"
  - "{{ media_storage_base_path }}/tv"
  - "{{ media_storage_base_path }}/movies"
  - "{{ media_storage_base_path }}/music"
```

**Note**: This role depends on `media_user` which detects UID/GID. Configure `media_user_user` and `media_user_group` in your playbook (see examples below).

**Permissions**: Directories are created with mode `750` (owner: rwx, group: r-x, other: none) for security. Media content is readable by the owner and group, but not world-readable.

## Dependencies

- `media_user` - Detects UID/GID from system user/group

This role is designed to be a dependency for media-related roles that need shared storage directories.

## Example Playbook

```yaml
- hosts: media_servers
  vars:
    # Configure user/group (UID/GID auto-detected)
    media_user_user: myuser
    media_user_group: mygroup
    # Configure storage paths
    media_storage_base_path: /mnt/storage
  roles:
    - media_storage
```

Most commonly, you won't include this role directly. Instead, it will be automatically included as a dependency when you use other media roles:

```yaml
- hosts: media_servers
  vars:
    # Configure user/group (UID/GID auto-detected)
    media_user_user: nobody
    media_user_group: nogroup
    # Configure storage paths
    media_storage_base_path: /storage
  roles:
    - plex       # Depends on media_storage -> media_user
    - sonarr     # Depends on media_storage -> media_user
    - radarr     # Depends on media_storage -> media_user
    - ombi       # Depends on media_user only (no folders needed)
```

## How It Works

1. This role depends on `media_user` which detects UID/GID from the system
2. This role is automatically included as a dependency by media roles that need storage (plex, sonarr, radarr, lidarr, transmission, sabnzbd)
3. It creates all required media directories with the proper user/group ownership
4. All media roles use the `media_user_uid` and `media_user_gid` facts (set by `media_user`) for their container PUID/PGID settings
5. This ensures all containers run with the same user permissions and can access shared directories

**Role dependency structure:**
- **Media roles with storage needs**: plex, sonarr, radarr, lidarr, transmission, sabnzbd, jackett
  - Depend on `media_storage` → which depends on `media_user`
  - Get UID/GID detection + folder creation
- **Media roles without storage needs**: ombi, prowlarr
  - Depend on `media_user` directly
  - Get UID/GID detection only

## Benefits

- **Simplified Configuration**: Set user/group once instead of per-role
- **Consistency**: All containers use the same PUID/PGID
- **Permission Management**: Directories are created with correct ownership automatically
- **Reduced Duplication**: Directory creation happens once, not in each role
- **Flexibility**: Easy to customize storage paths and permissions per deployment

## License

GPLv3

## Author Information

Jason Ernst
