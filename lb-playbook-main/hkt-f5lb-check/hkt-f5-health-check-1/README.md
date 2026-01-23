# F5 BIG-IP Health Check Automation with Ansible

This Ansible project performs automated health checks on F5 BIG-IP devices, generates reports in HTML and CSV format, and sends them via email.

## Project Structure

- `health_check_f5.yml`: The main playbook to execute.
- `inventory/`: Contains the `hosts.ini` file to define target F5 devices.
- `group_vars/`: Contains `all.yml` for global configuration (CyberArk, Email, etc.).
- `collections/`: Contains `requirements.yml` for required Ansible collections.
- `roles/f5_health_check/`: The role containing all the logic for the health checks and report templates.

## Configuration

1.  **Inventory**: Add your F5 BIG-IP devices to `inventory/hosts.ini` under the `[f5]` group.
2.  **Variables**: Edit `group_vars/all.yml` to configure your environment:
    *   `use_cyberark`: Set to `true` to fetch credentials from CyberArk or `false` to use the password defined in the inventory.
    *   `cyberark`: Update with your CyberArk API details if `use_cyberark` is true.
    *   `email`: Update with your SMTP server details and recipient list.
    *   `report_output_path`: Change the directory where reports will be saved on the Ansible controller.

## How to Run

This playbook is designed to be run from Red Hat Ansible Automation Platform (AAP).

1.  **Project Setup**: Create a new Project in AAP pointing to the Git repository containing this code.
2.  **Credential Setup**:
    *   Create a Machine Credential for connecting to the F5 devices (if not using CyberArk).
    *   Create a CyberArk AIM Credential if you are using CyberArk integration.
3.  **Job Template**: Create a Job Template that uses this project and the appropriate credentials.
    *   **Playbook**: Select `health_check_f5.yml`.
    *   **Inventory**: Select the inventory containing your F5 hosts.
4.  **Launch**: Launch the Job Template to run the health check. The reports will be generated and emailed to the configured recipients.