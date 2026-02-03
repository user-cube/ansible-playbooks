# Setup MacBook for DevOps Work

## Project structure

```
macos/
├── ansible.cfg          # Inventory path, deprecation_warnings
├── inventory.yml        # Explicit localhost (avoids Ansible warnings)
├── daily-driver.yml     # Main playbook
├── requirements.yml     # Galaxy collections
├── README.md
├── vars/
│   └── main.yml         # Configuration variables
├── handlers/
│   └── main.yml         # Yabai/skhd start and restart
└── tasks/               # Task files included by the playbook
    ├── preflight.yml
    ├── directories.yml
    ├── cli-apps.yml
    └── ...
```

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

From the `macos/` directory (so `ansible.cfg` and `inventory.yml` are found):

```bash
ansible-playbook daily-driver.yml -K
```

Pre-flight checks (Homebrew installed, macOS only) run automatically. If Homebrew is missing, the playbook fails with instructions to install it.

## Run only specific tasks (tags)

To install only AWS tools:

```bash
ansible-playbook daily-driver.yml -K --tags aws
```

Other useful tags: `cli-apps`, `kubernetes`, `git`, `editors`, `dotfiles`, etc. Pre-flight checks use tag `preflight` (and run by default); to skip them use `--skip-tags preflight`.

**Test CLI apps only:**

```bash
ansible-playbook daily-driver.yml -K --tags cli-apps
```

Verify: `which yabai skhd fzf zoxide bat jq yq rg`.

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

## Services (Yabai, skhd)

Yabai and skhd are started via **handlers** at the end of the play. They are notified when: laptop tools are installed (cli-apps), dotfiles `.config_macos` are synced (config reload), or when you run with tag `services`. Handlers are defined in `handlers/main.yml`. Start handlers are **idempotent**: they only start a service if it is not already running (using `pgrep`).

## Notes

Open neovim and run:

```nvim
:MasonInstallAll
```
