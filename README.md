# Cowrie Honeypot Setup with Ansible

This repository contains an Ansible playbook designed for the deployment and configuration of the Cowrie honeypot on a Debian-based system. Cowrie acts as a medium interaction SSH and Telnet honeypot, aiming to trap attackers by logging their interactions, commands, and behaviors.

## Prerequisites

Before running this playbook, ensure you have:
- An Ansible environment set up on your control machine.
- A target server running a Debian-based OS with SSH access configured.

## Setup Instructions

### 1. Clone the Repository

First, clone this repository to your control machine:

```bash
git clone [Your_Repository_URL]
cd [The_Clone_Directory]
```

### 2. Prepare the `secret.yml`

You need to create a `secret.yml` file that contains your target server's sudo password. This file should be encrypted with Ansible Vault for security:

```bash
ansible-vault create secret.yml
```

When prompted, enter a vault password. Then, in the editor that opens, input the following content, substituting `your_sudo_password` with the actual password:

```yaml
ansible_become_pass: your_sudo_password
```

Save and close the editor.

### 3. Running the Playbook

Execute the playbook against your inventory. If you haven't created an inventory file yet, create one according to Ansible's standards. Then, run:

```bash
ansible-playbook -i your_inventory_file setup_honeypot.yml --ask-vault-pass
```

Enter the vault password when prompted to decrypt `secret.yml`.

## Customizing the Deployment

- **Installation Directory**: The default installation path for Cowrie is set to `/opt/cowrie`. This can be adjusted by modifying the `cowrie_dir` variable within the playbook.
- **Configuration Files**: This playbook uses `cowrie.cfg` and `userdb.txt` from its `files` directory to configure Cowrie on the target server. Edit these files as necessary to match your deployment needs.

## Verifying the Installation

After the playbook execution, verify Cowrie's operation by checking the log files under `/opt/cowrie/var/log/cowrie/` on the target server. Additionally, attempt to SSH or Telnet to the target server using various credentials to see interactions logged.

## Contributing

Contributions to this playbook are welcome. Feel free to fork the repository, make improvements, and submit pull requests. For bugs or feature requests, please open an issue.

## License

This project is licensed under the MIT License - see the LICENSE.md file for details.

## Acknowledgments

- The Cowrie Community for developing and maintaining the honeypot software. Join their Slack channel for support and discussion: [https://www.cowrie.org/slack/](https://www.cowrie.org/slack/)
- Ansible for automating the deployment process.
