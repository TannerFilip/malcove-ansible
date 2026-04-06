# malcove-ansible

Ansible provisioning for **mal-box** — a Linux malware analysis workstation.

## Requirements

- Ansible 2.14+
- Target host running Debian/Ubuntu
- Root or passwordless-sudo access

## Usage

```bash
# Full provision
ansible-playbook playbooks/provision_malbox.yml

# Only install network tools
ansible-playbook playbooks/provision_malbox.yml --tags malbox_network

# Override YARA Forge tier (core | standard | extended)
ansible-playbook playbooks/provision_malbox.yml -e malbox_yara_forge_tier=core

# Check mode (dry run)
ansible-playbook playbooks/provision_malbox.yml --check
```

## Roles

| Role | Description | Tags |
|------|-------------|------|
| `malbox_base` | Base utilities, shell aliases, batcat symlink | `malbox_base` |
| `malbox_network` | Network analysis tools (tcpdump, tshark, nmap) | `malbox_network` |
| `malbox_reverse_engineering` | RE tools, capa (FLARE), Detect-It-Easy | `malbox_reverse_engineering` |
| `malbox_python_tools` | Python dev deps and analysis libraries via pip | `malbox_python_tools` |
| `malbox_node_tools` | Node.js and JavaScript analysis tools via npm | `malbox_node_tools` |
| `malbox_document_analysis` | Didier Stevens tools (pdfid, pdf-parser, oledump) | `malbox_document_analysis` |
| `malbox_yara` | YARA Forge community rulesets | `malbox_yara` |

## Key Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `malbox_base_install_dir` | `/opt` | Root installation directory |
| `malbox_base_bashrc_path` | `/root/.bashrc` | Shell config file to update |
| `malbox_yara_forge_tier` | `extended` | YARA Forge ruleset tier (`core`, `standard`, `extended`) |

See each role's `defaults/main.yml` for the full variable reference.

## Inventory

The default inventory targets `localhost` via a local connection. To provision a remote host:

```bash
ansible-playbook playbooks/provision_malbox.yml -i <host>, -u root
```
