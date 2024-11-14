# DevOps Infrastructure Project with Ansible

## Project Overview
This project demonstrates a robust infrastructure setup using Ansible for configuring, patching, monitoring, and securing Linux and Windows hosts. It includes CI/CD setup, application deployment, and incident alerting.

### Key Features:
- **Automated Infrastructure Setup** for Linux and Windows
- **Application Deployment** for both environments
- **Patching** automation for regular updates
- **Monitoring** and **Incident Alerting** setup using Prometheus and Grafana
- **Security Hardening** with Ansible roles

## Project Structure
The project follows best practices for Ansible directory organization:

```plaintext
project-root/
├── ansible.cfg                # Ansible configuration file
├── inventory/                 # Inventory files
│   ├── production             # Production environment inventory
│   ├── staging                # Staging environment inventory
│   └── dynamic_aws_inventory.yml  # Dynamic AWS inventory file
├── roles/                     # Roles for various configurations
│   ├── webserver              # Web server role
│   ├── database               # Database role
│   ├── monitoring             # Monitoring and logging role
│   ├── security               # Security configuration role
│   ├── patching               # System patching role
│   └── logging                # Logging configuration role
├── group_vars/                # Group variables
├── host_vars/                 # Host-specific variables
├── playbooks/                 # Playbooks for infrastructure setup
│   ├── site.yml               # Main playbook
│   ├── deploy_app.yml         # Application deployment playbook
│   └── ci_cd_pipeline.yml     # CI/CD pipeline setup playbook
└── README.md                  # Project documentation
```

### Installation and Setup
Clone the repository:
```bash
git clone <repository-url>
cd project-root
```
### Configure Secrets:
Use Ansible Vault to store sensitive variables in group_vars/all/vault.yml:

```bash
ansible-vault create group_vars/all/vault.yml
```
### Set up Inventory:
Modify inventory/production and inventory/staging with your specific hosts and credentials.

### Usage
Running the Main Playbook
To configure the entire infrastructure:
```bash
ansible-playbook playbooks/site.yml
```
### Deploying Applications
Use deploy_app.yml to deploy applications to Linux and Windows hosts:
```bash
ansible-playbook playbooks/deploy_app.yml
```
### Running CI/CD Setup
Use the following command to set up Jenkins and the CI/CD pipeline:
```bash
ansible-playbook playbooks/ci_cd_pipeline.yml
```

### Security Patch Management
To apply patches across all hosts:
```bash
ansible-playbook playbooks/site.yml --tags "patching"
```

### Testing and Linting
Lint Ansible code with ansible-lint:
```bash
ansible-lint playbooks/site.yml
```

### Test Roles with Molecule:
Go to the role directory and run Molecule tests:

```bash

cd roles/webserver
molecule test
```
### Tags for Task Control
This project includes tags to allow selective task execution. Here are some examples:

Patching only:
```bash
ansible-playbook playbooks/site.yml --tags "patching"
```
Deployment tasks only:
```bash
ansible-playbook playbooks/site.yml --tags "deploy"
```
### Roles Documentation
Webserver Role
This role installs and configures the web server. Key variables:

web_port: Port for the web server (default: 80)
app_list: List of applications to install or remove

### Database Role 
Installs and configures PostgreSQL with basic setup.

### Security Role
Configures firewall and system security policies. Configurable through:

security_policy: Security policy level (e.g., 'strict')

### Monitoring and Logging Role
Sets up Prometheus, Grafana, and configures logging with alerting capabilities for incidents.

### Alerts and Notifications
Incident alerts are configured for critical events. Slack notifications can be triggered by setting vault_slack_token in group_vars/all/vault.yml.
