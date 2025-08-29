# Molecule Testing

This project uses [Molecule](https://molecule.readthedocs.io/) for testing Ansible roles.

## Prerequisites

- Docker
- Python 3.8+

## Installation

Install the required dependencies:

```bash
pip install -r requirements.txt
```

## Running Tests

### Test a specific role

```bash
cd roles/plex
molecule test
```

### Test all roles with molecule configurations

```bash
# Currently available: plex
for role in roles/*/molecule; do
    cd $(dirname $role)
    echo "Testing $(basename $(dirname $role))..."
    molecule test
    cd ../..
done
```

## Test Structure

Each role with molecule testing has the following structure:

```
roles/<role_name>/
├── molecule/
│   └── default/
│       ├── molecule.yml      # Molecule configuration
│       ├── converge.yml      # Test playbook
│       ├── verify.yml        # Verification tests
│       └── prepare.yml       # Environment preparation
├── tasks/
├── defaults/
└── meta/
```

## GitHub Actions

The project includes automated testing via GitHub Actions that runs:
- ansible-lint for all YAML files
- molecule tests for roles with molecule configurations

## Available Test Roles

- **plex**: Tests Plex media server deployment and configuration