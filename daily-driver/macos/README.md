# Setup MacBook for DevOps Work

## Install homebrew 

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## Install Ansible

```bash
brew install ansible
```

## Execute playbook

```bash
ansible-playbook daily-driver.yml -K
```

## Notes

Open neovim and execute the following command:

```nvim
:MasonInstallAll
```
