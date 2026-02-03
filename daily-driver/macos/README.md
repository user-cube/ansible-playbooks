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

O playbook usa as collections `community.general` (homebrew, homebrew_cask, homebrew_tap) e `ansible.posix` (synchronize para dotfiles):

```bash
ansible-galaxy collection install -r requirements.yml
```

## Execute playbook

```bash
ansible-playbook daily-driver.yml -K
```

## Executar apenas algumas tasks (tags)

Para instalar só as ferramentas AWS:

```bash
ansible-playbook daily-driver.yml -K --tags aws
```

Outras tags úteis: `cli-apps`, `kubernetes`, `git`, `editors`, `dotfiles`, etc.

## Dotfiles

As tasks de dotfiles clonam o repositório, criam `~/.config` se não existir e copiam/sincronizam ficheiros de forma **idempotente** (só alteram o que mudou). Para usar outro repositório:

```bash
ansible-playbook daily-driver.yml -K --tags dotfiles -e "dotfiles_repo=https://github.com/teu-user/dotfiles.git"
```

## Testar a AWS

Depois de correr as tasks com tag `aws`, verifica as instalações:

```bash
aws --version
eksctl version
aws-iam-authenticator version
granted --version
```

## Notes

Open neovim and execute the following command:

```nvim
:MasonInstallAll
```
