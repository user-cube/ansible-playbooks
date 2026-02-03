# Setup MacBook for DevOps Work

## Install homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## Install Ansible

```bash
brew install ansible
```

## Install Ansible Galaxy collections

The playbook uses the `community.general` collection (homebrew, homebrew_cask, homebrew_tap) and `ansible.posix` (synchronize for dotfiles):

```bash
ansible-galaxy collection install -r requirements.yml
```

## Run the playbook

```bash
ansible-playbook daily-driver.yml -K
```

## Run only specific tasks (tags)

To install only AWS tools:

```bash
ansible-playbook daily-driver.yml -K --tags aws
```

Other useful tags: `cli-apps`, `kubernetes`, `git`, `editors`, `dotfiles`, etc.

## Configuration variables

Variables are defined in **`vars/main.yml`** (dotfiles repo, directories, NvChad, Powerlevel10k, fonts, custom go tools). To override without editing the file:

```bash
# Different dotfiles repository
ansible-playbook daily-driver.yml -K --tags dotfiles -e "dotfiles_repo=https://github.com/your-user/dotfiles.git"

# Different directories in $HOME (YAML list)
ansible-playbook daily-driver.yml -K --tags directories -e '{"directories_to_create": ["personal", "work", "hooks", "projects"]}'
```

## Dotfiles

Dotfiles tasks clone the repository defined in `vars/main.yml`, create `~/.config` if missing, and copy/sync files in an **idempotent** way. To use a different repository, set the `dotfiles_repo` variable (see above).

## Test fonts

To install only the MesloLGS fonts (Powerlevel10k):

```bash
ansible-playbook daily-driver.yml -K --tags fonts
```

Verify: `ls ~/Library/Fonts/MesloLGS*` or open Font Book and search for "MesloLGS".

## Test AWS

After running the tasks with tag `aws`, verify the installations:

```bash
aws --version
eksctl version
aws-iam-authenticator version
granted --version
```

## Notes

Open neovim and run:

```nvim
:MasonInstallAll
```
