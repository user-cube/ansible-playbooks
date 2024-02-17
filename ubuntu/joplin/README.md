# Joplin Installation and Uninstallation

This set of Ansible playbooks automates the installation and uninstallation of Joplin, a note-taking application, on Ubuntu systems.

## Installation

### Prerequisites

Ensure that Ansible is installed on your system.

### Steps

1. **Download Joplin Installation Script:**
   - The `install_joplin.yaml` playbook downloads the Joplin installation script from the official GitHub repository.

2. **Set Execute Permissions:**
   - The playbook sets execute permissions for the downloaded installation script.

3. **Execute Installation Script:**
   - The playbook executes the Joplin installation script to install the application and its dependencies.

To install Joplin, run the `install_joplin.yaml` playbook using the following command:

```bash
ansible-playbook install_joplin.yaml
```

## Uninstallation

### Steps

1. **Remove Joplin Directory:**
   - The `uninstall_joplin.yaml` playbook removes the Joplin directory (`~/.joplin/`).

2. **Remove Desktop Icons and Icons:**
   - The playbook removes Joplin desktop icons and associated icon files.

3. **Update Desktop Database:**
   - The playbook updates the desktop database for applications and icons.

To uninstall Joplin, run the `uninstall_joplin.yaml` playbook using the following command:

```bash
ansible-playbook uninstall_joplin.yaml
```
