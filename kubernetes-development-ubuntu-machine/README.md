# Kubernetes Local Setup

This repository contains an Ansible playbook for setting up Kubernetes locally using Minikube. It also installs the K9s CLI tool for interacting with the Kubernetes cluster.

## Prerequisites

- Ansible
- A Linux-based system with sudo privileges

## Usage

1. Clone this repository.
2. Run the Ansible playbook:

```bash
ansible-playbook kubernetes-local.yml
```

## What does the playbook do?

- Installs required packages for Minikube and K9s.
- Adds the Kubernetes apt repository and its key.
- Downloads and installs Minikube.
- Starts Minikube with Docker as the driver.
- Enables the Ingress addon in Minikube.
- Sets up aliases for `kubectl` in both bash and zsh shells.
- Downloads and installs the latest version of K9s.

## Note

This playbook assumes that the user's shell is either bash or zsh. If you're using a different shell, you may need to manually add the `kubectl` aliases to your shell's configuration file.
