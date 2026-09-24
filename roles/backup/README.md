# zephyr82.fhem backup Role

role for backing up specific files from a running FHEM server

## Requirements

none

## Role Variables

The following table provides an overview of all settable variables for this role, including their descriptions, types, default values, and whether they are required.

| Variable | Type | Default | Required | Description |
|----------|------|---------|----------|-------------|
| backup_fhem_server | str | "" | Yes | DNS name of the FHEM server to backup. If not specified, role execution will fail. |
| backup_path | str | "backup/" | No | Path where the backup files will be stored. Notice the trailing slash, which is important for correct path concatenation. |
| backup_files | list of dict | See below | No | List of files and directories to backup. Each item should be a dictionary with keys 'file_path' and 'preserve_permissions'. |

The `backup_fhem_server` should, but has not to be a different server than the server this role runs on. 

**Default value for backup_files:**
```yaml
- file_path: "/opt/fhem/fhem.cfg"
  preserve_permissions: true
- file_path: "/opt/fhem/log/fhem.save"
  preserve_permissions: true
```

**Sub-options for backup_files items:**
| Variable | Type | Default | Required | Description |
|----------|------|---------|----------|-------------|
| file_path | str | - | Yes | Path to the file or directory to backup. |
| preserve_permissions | bool | true | No | Whether to preserve the original permissions of the file or directory during backup.

## Dependencies

none

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- name: Execute tasks on servers
  hosts: fhem
  roles:
    - role: zephyr82.fhem.backup
```

Another way to consume this role would be:

```yaml
- name: Configure FHEM hosts
  hosts: fhem
  remote_user: kblocal
  tasks:
    - name: Start installing FHEM
      ansible.builtin.include_role:
        name: zephyr82.fhem.installation
      tags:
        - fhem_installation
    - name: Backup FHEM configuration
      ansible.builtin.include_role:
        name: zephyr82.fhem.backup
      tags:
        - fhem_backup
        - debug
    - name: Restore FHEM configuration
      ansible.builtin.include_role:
        name: zephyr82.fhem.restore
      tags:
        - fhem_restore
        - debug
```

## Role Idempotency

Designation of the role as idempotent (True/False)

## Role Atomicity

Designation of the role as atomic if applicable (True/False)

## Roll-back capabilities

Define the roll-back capabilities of the role

## License

<!-- TO-DO: Update the license to the one you want to use (delete this line after setting the license) -->
BSD
