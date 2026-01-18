# Media User Role

This role detects the UID and GID for a specified system user and group, making them available to all media-related roles as Ansible facts.

## Purpose

The `media_user` role serves as a foundational dependency for all media-related roles, providing:
- Automatic UID/GID detection from system users
- Consistent PUID/PGID settings across all media containers
- Single point of configuration for container user permissions

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
# User and group names - MUST exist on the target system before running this role
# The UID and GID will be automatically detected from these at runtime
# Common choices: nobody/nogroup (most systems), media/media (custom), your username
media_user_user: nobody
media_user_group: nogroup
```

**IMPORTANT:** The specified user and group must already exist on the target system. The role will fail if they don't exist. Use `nobody`/`nogroup` for a safe default available on most systems, or create a dedicated media user beforehand.

The role automatically sets these facts (do not configure these manually):
- `media_user_uid` - The detected UID
- `media_user_gid` - The detected GID

## Dependencies

None. This role is designed to be a dependency for other media-related roles.

## Example Playbook

```yaml
- hosts: media_servers
  vars:
    # Specify the user/group - UID/GID are auto-detected
    media_user_user: nobody
    media_user_group: nogroup
  roles:
    - media_user
```

Most commonly, you won't include this role directly. It's automatically included as a dependency:

```yaml
- hosts: media_servers
  vars:
    media_user_user: nobody
    media_user_group: nogroup
  roles:
    - plex       # Depends on media_storage -> media_user
    - sonarr     # Depends on media_storage -> media_user
    - ombi       # Depends on media_user directly
    - prowlarr   # Depends on media_user directly
```

## How It Works

1. Uses `getent` module to query the system's passwd database for the user
2. Uses `getent` module to query the system's group database for the group
3. Extracts the UID and GID from the query results
4. Sets `media_user_uid` and `media_user_gid` as Ansible facts
5. These facts are available to all subsequent roles in the playbook

## Role Types

- **Roles that need media folders** (plex, sonarr, radarr, lidarr, transmission, sabnzbd):
  - Depend on `media_storage` (which depends on `media_user`)
  - Get UID/GID detection + folder creation

- **Roles that don't need media folders** (ombi, prowlarr, jackett):
  - Depend on `media_user` only
  - Get UID/GID detection without folder creation

## Benefits

- **Automatic Detection**: No need to manually look up or specify UID/GID
- **Consistency**: All containers use the same PUID/PGID automatically
- **Portability**: Playbooks work across different systems with different UIDs
- **Simplicity**: Only specify username/group, everything else is automatic

## License

GPLv3

## Author Information

Jason Ernst
