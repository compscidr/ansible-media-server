# Molecule Testing

This project uses [Molecule](https://molecule.readthedocs.io/) for testing Ansible roles.

## Prerequisites

- Docker
- Python 3.8+

## Installation

### For Local Development (Recommended)

Create and activate a virtual environment, then install dependencies:

```bash
# Create a virtual environment
python3 -m venv venv

# Activate the virtual environment
source venv/bin/activate  # On Linux/macOS
# or
venv\Scripts\activate     # On Windows

# Install the required dependencies
pip install -r requirements.txt
```

### Global Installation (Not Recommended)

Alternatively, you can install globally (not recommended for local development):

```bash
pip install -r requirements.txt
```

## Running Tests

### Test all roles

All roles are tested together using the centralized molecule configuration:

```bash
# Make sure you're in the project root directory
molecule test
```

### Test specific scenarios

```bash
# Run only the converge step (deploy all roles)
molecule converge

# Run only verification tests
molecule verify

# Clean up test environment
molecule destroy
```

## Test Structure

The project uses a centralized molecule configuration:

```
.
├── molecule/
│   └── default/
│       ├── molecule.yml      # Molecule configuration
│       ├── converge.yml      # Test playbook that includes all roles
│       ├── verify.yml        # Verification tests for all services
│       └── prepare.yml       # Environment preparation
└── roles/
    ├── plex/
    ├── ombi/
    ├── radarr/
    └── ...                   # All roles are tested together
```

## GitHub Actions

The project includes automated testing via GitHub Actions that runs:
- ansible-lint for all YAML files
- molecule tests for roles with molecule configurations

## Tested Roles

The molecule tests verify the deployment and configuration of all media server roles:

- **plex**: Plex media server
- **ombi**: Request management
- **radarr**: Movie management
- **sonarr**: TV show management  
- **lidarr**: Music management
- **prowlarr**: Indexer management
- **jackett**: Torrent indexer proxy
- **sabnzbd**: Usenet downloader
- **flaresolverr**: Cloudflare solver
- **transmission**: BitTorrent client