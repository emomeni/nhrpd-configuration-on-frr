# Ansible Playbook: Enable NHRPD on Servers with FRR Installed
This Ansible playbook automates the process of enabling the Next Hop Resolution Protocol Daemon (NHRPD) on servers that have the Free Range Routing (FRR) package installed. The playbook checks for FRR installation, modifies the necessary configuration files to enable NHRPD, and ensures that the NHRPD service is running.

## Table of Contents
- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Variables](#variables)
- [Playbook Tasks](#playbook-tasks)
- [Verification](#verification)
- [Troubleshooting](#troubleshooting)
- [License](#license)

## Introduction
This playbook performs the following actions:

1. Checks if the FRR package is installed on the target servers.
2. Modifies the FRR configuration files to enable `nhrpd`.
3. Ensures the `nhrpd` service is running and enabled on system boot.

## Prerequisites
- Ansible installed on your control node.
- SSH access to the target servers.
- Sudo privileges on the target servers for the user running the playbook.
- The target servers must have the FRR package installed.

## Installation
1. Clone this repository or download the playbook file:
```bash
   git clone https://github.com/yourusername/ansible-enable-nhrpd.git
   cd ansible-enable-nhrpd
```
2. Ensure your inventory file is set up correctly. Update the `inventory` file with the list of target servers.
3. (Optional) Modify the `nhrpd_config.yaml` playbook file to suit your environment, especially if using different file paths or configurations.

## Usage
Run the playbook with the following command:
```bash
ansible-playbook -i your_inventory_file nhrpd_config.yaml
```
Replace `your_inventory_file` with the path to your Ansible inventory file.

## Variables
The following variables are defined in the playbook and can be customized:
* `frr_conf_path`: Path to the main FRR configuration file (default: `/etc/frr/frr.conf`)
* `nhrpd_conf_path`: Path to the nhrpd configuration file (default: `/etc/frr/nhrpd.conf`)

To override these variables, you can pass them directly via the command line:
```bash
ansible-playbook -i your_inventory_file nhrpd_config.yaml -e "frr_conf_path=/custom/path/frr.conf"
```

## Playbook Tasks
* Check if FRR is installed: Verifies if the FRR package is present on the target server.
* Enable nhrpd in FRR configuration: Adds or updates the `nhrpd` configuration in the FRR configuration file.
* Create nhrpd configuration file if not present: Creates a default `nhrpd` configuration file if it does not exist.
* Ensure nhrpd is enabled in the FRR daemons file: Ensures `nhrpd` is enabled in the `/etc/frr/daemons` file.
* Start and enable nhrpd service: Restarts the FRR service to apply changes and ensures it is enabled on boot.
* Verify nhrpd service is running: Checks that the FRR service is active and running.

## Verification
After running the playbook, verify that `nhrpd` is enabled and running with the following command:
```bash
systemctl status frr
```
The output should indicate that the service is `active (running)`.

## Troubleshooting
* FRR Not Installed: Ensure that the FRR package is installed on the target servers before running the playbook.
* Permission Denied: Ensure the user running the playbook has sudo privileges on the target servers.
* Service Not Running: Verify that the `nhrpd` configuration is correct and that there are no syntax errors in the configuration files.

## License
This project is licensed under the MIT License - see the LICENSE file for details.



# Explanation of the README.md Structure
1. **Introduction**: Brief overview of what the playbook does.
2. **Prerequisites**: Lists the requirements needed to run the playbook.
3. **Installation**: Instructions on how to set up and prepare the playbook.
4. **Usage**: Provides a command to run the playbook using Ansible.
5. **Variables**: Describes configurable variables used within the playbook and how to override them.
6. **Playbook Tasks**: Summarizes the main tasks the playbook will perform.
7. **Verification**: How to confirm that `nhrpd` is enabled and running.
8. **Troubleshooting**: Common issues and solutions related to the playbook.
9. **License**: Licensing information for the project.

Feel free to modify this `README.md` to better match your repository's structure and specific needs.
