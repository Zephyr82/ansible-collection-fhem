# Role Name

The role to restore specific files onto a (new) FHEM server after making a backup from another (old) FHEM server. In order to use this role you MUST have used the backup role at first. It is also important to notice that you have to made a backup with the potential new server as a target host because

## Requirements

none

## Role Variables

The following table provides an overview of all settable variables for this role, including their descriptions, types, and default values.

| Variable | Type | Default | Description |
|----------|------|---------|-------------|
| run_my_variable | str | "default_value" | A simple string argument for demonstration.

## Dependencies

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

## Example Playbook

A complete role for setting up an existing server with FHEM, making a backup from an old (running) FHEM server and pushing all neccessary files onto the new one.

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

## License

BSD
