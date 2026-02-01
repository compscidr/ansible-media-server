# Changelog

## [1.2.0] - 2026-01-31

### Added
- **New `slskd` role**: Installs and configures the slskd container (Soulseek client)
  - Web-based interface for Soulseek peer-to-peer music sharing
  - Configurable ports for web UI (5030/5031) and Soulseek (50300)
  - Integrates with media_storage for consistent paths and permissions

- **New `soularr` role**: Installs and configures the soularr container
  - Bridges slskd and Lidarr for automated music downloads
  - Monitors Lidarr's wanted list and searches slskd automatically

## [1.1.0] - 2026-01-31

### Added
- **New `media_user` role**: Automatically detects UID/GID from system user/group
  - Uses `getent` to query system passwd and group databases
  - Sets `media_user_uid` and `media_user_gid` as Ansible facts
  - Eliminates need to manually specify PUID/PGID values

- **New `media_storage` role**: Creates shared media directories with proper ownership
  - Depends on `media_user` for UID/GID detection
  - Creates configurable media directories (downloads, tv, movies, music, etc.)
  - Ensures consistent permissions across all media containers

- **All roles**: Added Docker network support for container name resolution
  - Added `<role>_networks` variable to all roles (e.g., `sonarr_networks`, `radarr_networks`)
  - Allows containers to be connected to custom Docker networks
  - Enables containers to communicate by name instead of IP address

- **Plex**: Added `plex_network_mode` variable (default: "bridge")
  - Set to "host" for DLNA/UPnP discovery features
  - Bridge mode allows container name resolution with custom networks

### Changed
- **All media roles**: Now use automatic UID/GID detection
  - Roles with storage needs (plex, sonarr, radarr, lidarr, transmission, sabnzbd, jackett) depend on `media_storage`
  - Roles without storage needs (ombi, prowlarr) depend on `media_user` only
  - All roles use `media_user_uid` and `media_user_gid` for container PUID/PGID
  - Removed hardcoded UID/GID defaults from individual role defaults

- **Configuration simplified**: Users now only specify `media_user_user` and `media_user_group`
  - UID/GID are automatically detected at runtime

- **Plex**: Simplified role from 4 duplicate tasks to 1 dynamic task
  - Devices (dri/dvb) now handled dynamically instead of separate task variants

## [1.0.7] - 2026-01-17
- **Lidarr**: Added `lidarr_plugins` variable to enable using the hotio plugins image (ghcr.io/hotio/lidarr:pr-plugins) instead of the default linuxserver image

## [1.0.6] = 2026-01-17
- Fixed paths to prevent overlapping mounts

## [1.0.5] - 2026-01-17
- Fixed paths for radarr, sonarr, lidarr wrt transmission so that remote mappings 
  aren't required (the -arrs expect transmission downloads in /data)

## [1.0.4] - 2026-01-17
- Transmission: Added a peer port to the exposed ports

## [1.0.3] - 2026-01-05

### Added
- **All roles**: Added memory_swap support to prevent Docker memory limit errors
  - Added `*_memory_swap` parameters to all role defaults
  - Prevents "Memory limit should be smaller than memoryswap limit" errors
  - Memory swap set equal to memory limit to disable swap for better performance

### Changed
- **Sonarr**: Changed hardcoded memory value to use variable
  - Added `sonarr_memory` and `sonarr_memory_swap` parameters for consistency
  - Now follows the same pattern as other roles

## [1.0.2] - 2026-01-05

### Added
- **Transmission**: Added memory limit support
  - Added `transmission_memory` parameter to role defaults (default: "1g")
  - Container deployments now respect memory limits for better resource management

## [1.0.1] - 2026-01-05

### Fixed
- **SABnzbd**: Removed nested `/config/Downloads` mount in SABnzbd role
  - Changed downloads mount from `/config/Downloads` to `/downloads`
  - Ensures SABnzbd and *arr apps see downloads at consistent paths
  - Prevents same nested mount issues that affected Sonarr/Radarr/Lidarr

## [1.0.0] - 2026-01-05

### Breaking Changes
- **BREAKING**: Fixed variable name typos - `tranmissions` → `transmissions`, `downoads` → `downloads`
  - Affected variables: `sonarr_transmissions_downloads_folder`, `sonarr_sabnzbd_downloads_folder`, and similar for radarr/lidarr
  - Users must update their playbooks to use corrected variable names

### Fixed
- **Critical**: Removed nested mount configuration that was causing database corruption issues
  - Changed `/config/Downloads` mount to `/downloads` to avoid nesting under `/config`
  - This resolves authentication persistence issues where user credentials were being lost
  - Fixed typo: `/configs/Downloads/complete` → `/downloads/complete`
- Updated all role defaults to use consistent, non-nested download paths
- Fixed documentation in README files to reflect corrected variable names

### Changed
- Simplified volume mount structure for sonarr, radarr, and lidarr roles
- Downloads now mounted at `/downloads` instead of nested under `/config`

## Previous Releases

- fix an issue with undefined install_docker variable
- added molecule tests
- added lidarr and updated plex with a music directory
- removed dependency to install docker
- updating to pass ansible-lint
