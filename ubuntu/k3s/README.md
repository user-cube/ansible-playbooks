# Ansible Playbook: Install Kubernetes Locally

This Ansible playbook automates the installation of Kubernetes locally using k3s, as well as additional tools such as k9s and Helm.

## Requirements

- Ansible installed on the control machine
- `sudo` privileges on the target machine
- Internet access on the target machine

## How to Use

1. Clone this repository:

```bash
git clone https://github.com/user-cube/ansible-playbooks.git
```

2. Navigate to the playbook directory:

```bash
cd ubuntu/k3s/
```

3. Edit the `hosts` file to specify the target host where you want to install Kubernetes locally.

4. Run the playbook:

```bash
ansible-playbook k3s.yml
```

5. Once the playbook execution is complete, you should have Kubernetes installed locally, along with k9s and Helm.

## Customization

- Modify the playbook variables as needed to customize the installation process.
- Adjust the playbook tasks to suit your environment and requirements.

## Notes

- This playbook assumes you are running it on a Linux-based system.
- Ensure you have sufficient permissions and network access for the installation process to complete successfully.
- Review the playbook tasks and verify they meet your security and operational requirements.
