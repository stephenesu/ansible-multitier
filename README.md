# Ansible Multitier Project Automation

This repository contains an Ansible multitier automation project that deploys a Node.js application with a three-tier architecture across three virtual machines:

* **Webserver** – Hosts Apache2 configured as a reverse proxy
* **Appserver** – Hosts the Node.js application
* **Database server** – Hosts MariaDB for the application

# Project Structure

```
ansible-multitier/
├── ansible.cfg                # Ansible configuration
├── collections/               # Custom and third-party collections
├── group_vars/                # Variables for each group of hosts
│   ├── appserver.yml
│   ├── database.yml
│   └── webserver.yml
├── inventory.ini              # Hosts inventory
├── playbook.yml               # Main playbook for deployment
├── requirements.yml           # Ansible Galaxy role dependencies
└── roles/                     # Roles for each tier and external roles
    ├── appserver
    ├── database
    ├── geerlingguy.apache
    ├── geerlingguy.php
    └── webserver
```

# Securing Secrets

Sensitive information such as database passwords or API keys is stored in **Vault-encrypted variable files** in `group_vars`.

* To encrypt a file:

```bash
ansible-vault encrypt group_vars/database.yml
```

* To run a playbook using Vault:

```bash
ansible-playbook playbook.yml --ask-vault-pass
```

This ensures that secret keys remain secure while deploying your infrastructure.

## Running the Project

1. Update `inventory.ini` to reflect the IP addresses of your webserver, appserver, and database server.
2. Execute the main playbook, providing the Vault password for encrypted variables:

```bash
ansible-playbook playbook.yml --ask-vault-pass
```

This will provision and configure all three tiers automatically.

If you want, I can also **add a small diagram showing the flow: Webserver → Appserver → Database** to make it visually clear. This is especially helpful for documentation or sharing with others. Do you want me to add that?
