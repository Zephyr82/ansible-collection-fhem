# Role Name

The role to restore specific files onto a (new) FHEM server after making a backup from another (old) FHEM server. In order to use this role you MUST have used the backup role at first. It is also important to notice that you restore from a file hierarchy like `<backup_path>/<filename>/<backup_fhem_server>/path/to/file`.
Which files to restore is saved as a json file under the path of the variable `restore_path`. The json file is named after the `backup_fhem_server`, e.g. `fhem.example.com.json`. Or in other words: Which files get restore is directly controlled by the contents of the variable `backup_files`. Every file to backup (and restore) is documented in the json file and the role `restore` restores every file in the json file.

## Requirements

none

## Role Variables

The following table provides an overview of all settable variables for this role, including their descriptions, types, and default values.

The variables `restore_path` from the role `restore` and `backup_path` from role `backup` are semantically the same path. The first is the one the files get backed up into, the second ist the one the file get read from. When backuping up from the server fhem.example.com, while setting `backup_path: "temp/backup/"` the path will look something like `temp/backup/fhem.cfg/fhem.example.com/opt/fhem/fhem.cfg`. If you want to take that backup files and copy them over to your new FHEM server, you should set the variable `restore_path: "{{ backup_path}}"` or explicitly `restore_path: "temp/backup/"`. You MUST set the variable `backup_fhem_server` so the full path for each file gets properly expanded.

| Variable | Type | Default | Description |
|----------|------|---------|-------------|
| run_my_variable | str | "default_value" | A simple string argument for demonstration.

## Dependencies

none

## Example Playbook

A complete role for setting up an existing server with FHEM, making a backup from an old (running) FHEM server and pushing all neccessary files onto the new one.

```yaml
- name: Configure FHEM hosts
  hosts: fhem
  remote_user: kblocal
  vars:
    backup_path: "temp/backup"
    restore_path: "{{ backup_path }}"
    backup_fhem_server: fhem.example.com
    backup_files:
      - file_path: "/opt/fhem/fhem.cfg"
        preserve_permissions: true
  tasks:
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
