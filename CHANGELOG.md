# Changelog

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