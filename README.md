# ansible-zsh

Installs and configures zsh across Debian/Ubuntu, RHEL/Fedora, and Arch Linux.

## Structure
```
ansible-zsh/
├── ansible.cfg
├── playbook.yml
├── group_vars/
│   └── all.yml
├── inventory/
│   └── hosts.ini
└── roles/
    └── zsh/
        ├── tasks/
        │   ├── main.yml
        │   ├── install.yml
        │   └── remove.yml
        └── handlers/
            └── main.yml
```

## Variables

| Variable | Default | Description |
|---|---|---|
| `zsh_action` | `install` | `install` or `remove` |
| `zsh_user` | `$SUDO_USER` | User to configure zsh for |
| `zsh_set_default_shell` | `true` | Set zsh as the default shell |
| `install_oh_my_zsh` | `false` | Also install Oh My Zsh |
| `zsh_zshrc_source` | `""` | Path to a local `.zshrc` to copy |

## Commands
```bash
# Install zsh
ansible-playbook playbook.yml

# Install zsh + Oh My Zsh (includes zsh-autosuggestions and zsh-syntax-highlighting)
ansible-playbook playbook.yml -e "install_oh_my_zsh=true"

# Install with a custom .zshrc
ansible-playbook playbook.yml -e "zsh_zshrc_source=files/.zshrc"

# Install everything
ansible-playbook playbook.yml -e "install_oh_my_zsh=true" -e "zsh_zshrc_source=files/.zshrc"

# Install for a specific user
ansible-playbook playbook.yml -e "zsh_user=mag"

# Remove zsh
ansible-playbook playbook.yml -e "zsh_action=remove"

# Dry run
ansible-playbook playbook.yml --check

# Verbose output
ansible-playbook playbook.yml -v
```

## WSL note

Changing the default shell via Ansible does not take effect in WSL terminals.
Add this to `~/.bashrc` instead:
```bash
echo "exec zsh" >> ~/.bashrc
```
