# Ansible Interactive Storage Management

This repository contains a suite of interactive Ansible playbooks designed to automate Linux storage operations. The toolkit facilitates complex tasks such as Logical Volume Manager (LVM) expansion, disk formatting, and persistent mount management through a guided, command-line interface.

The primary objective of these playbooks is to reduce human error during critical storage modifications by implementing pre-execution safety checks and structured user prompts.

## Key Features

* **Operational Safety:** Includes strict conditional checks to prevent accidental modification or formatting of system roots (e.g., `/dev/sda`, active root partitions).
* **Interactive Workflow:** Utilizes Ansible's `vars_prompt` to dynamically request target devices, sizes, and mount points at runtime, eliminating the need for hardcoded inventory variables.
* **LVM Automation:** Streamlines the process of extending Volume Groups and Logical Volumes, including cross-disk expansion and immediate filesystem resizing.
* **Persistence Management:** Automates the configuration of `/etc/fstab` for permanent mounts, handling UUID retrieval and backup generation automatically.
* **Disk Analysis:** Provides utilities for scanning SCSI buses and reporting on disk topology and partition status.

## Playbook Overview

| Playbook | Description |
| :--- | :--- |
| `mount_fstab.yml` | Mounts block devices and manages `/etc/fstab` entries. Supports UUID-based persistence and automatic filesystem type detection. |
| `increase_lvm.yml` | Performs advanced LVM expansion. Capable of analyzing storage availability, adding new physical disks to Volume Groups, and resizing logical volumes. |
| `format_and_umount_disk.yml` | Handles unmounting, partition formatting, and full disk wiping. Includes "fail-safe" mechanisms to protect the operating system drive. |
| `lvm_mount_simple.yml` | A streamlined workflow for creating, formatting, and mounting new Logical Volumes in a single execution. |
| `scan_list_simple.yml` | Scans the host for new storage devices and lists unpartitioned candidates suitable for configuration. |
| `disk_status.yml` | Generates a comprehensive report on current disk usage, mount points, and LVM hierarchy. |

## Prerequisites

* **Ansible:** Version 2.9 or higher.
* **Privileges:** Root access (sudo) is required on the target host.
* **Python:** Python 3 interpreter on the target host.

## Installation

1.  Clone the repository:
    ```bash
    git clone [https://github.com/berke44gulec/ansible-interactive-storage.git](https://github.com/berke44gulec/ansible-interactive-storage.git)
    cd ansible-interactive-storage
    ```

2.  Install the required Ansible collections:
    ```bash
    ansible-galaxy collection install -r requirements.yml
    ```

## Usage

Execute the desired playbook using the `ansible-playbook` command. The system will prompt for necessary inputs.

**Example: Extending an LVM Volume**
```bash
ansible-playbook increase_lvm.yml
````

**Example: Mounting a Device Persistently**

```bash
ansible-playbook mount_fstab.yml
```

## Disclaimer and Liability

These scripts perform destructive operations on storage devices. While safety mechanisms are implemented to protect system drives, the user assumes full responsibility for data integrity.

  * Always verify backups before performing format or wipe operations.
  * Review the code to ensure it meets the specific requirements of your environment before execution.

## License

This project is licensed under the MIT License.
