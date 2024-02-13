# Setup Ubuntu Machine for Work

This Ansible playbook automates the setup process for an Ubuntu machine tailored for work environments. It installs various tools commonly used by developers and system administrators.

## Usage

1. Ensure Ansible is installed on your local machine.
2. Create an inventory file with your localhost or target machine.
3. Run the playbook using the command:
    ```
    ansible-playbook -i <inventory_file> setup_ubuntu_for_work.yaml
    ```

## Tasks

### Update package index

- Updates the package index using `apt`.

### Install Visual Studio Code

- Adds Microsoft GPG key and repository.
- Installs Visual Studio Code via `apt`.
- Adds VSCode to the system PATH.

### Install Docker

- Installs Docker prerequisites.
- Adds Docker's official GPG key and repository.
- Installs Docker CE via `apt`.
- Starts and enables the Docker service.
- Creates a Docker group and adds the current user to it.

### Install Termius

- Downloads and installs the Termius .deb package.

### Install Postman

- Installs Postman via Snap.

### Install jq

- Installs jq JSON processor via `apt`.

### Install nektos/act

- Creates a directory for the act binary.
- Retrieves the latest release URL from GitHub API.
- Downloads and extracts the act binary.
- Sets executable permissions for the act binary.

### Install Joplin

- Installs libfuse2 prerequisite.
- Downloads the Joplin installation script.
- Sets execute permissions for the installation script.
- Executes the Joplin installation script.
