# zephyr82.fhem run Role

A brief description of the role goes here.

## Requirements

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

## Role Variables

The following table provides an overview of all settable variables for this role, including their descriptions, types, and default values.

| Variable | Type | Default | Description |
|----------|------|---------|-------------|
| installation_pre_install_packages | list | See below | List of packages to install before the main installation. |
| installation_packages | list | See below | List of FHEM-related packages to install. |
| installation_apt_key_url | str | "https://debian.fhem.de/archive.key" | URL for the FHEM repository GPG key. |
| installation_apt_key_path | str | "/usr/share/keyrings/debianfhemde-archive-keyring.gpg" | Path where the GPG key will be stored. |
| installation_temp_apt_key_dest | str | "/tmp/debianfhemde-archive.key" | Temporary destination for the downloaded GPG key. |
| installation_apt_sources_file_path | str | "/etc/apt/sources.list.d/debianfhemde.sources" | Path for the APT sources file. |
| installation_apt_url | str | "https://debian.fhem.de/nightly/" | URL for the FHEM APT repository. |

**Default value for installation_pre_install_packages:**
```yaml
- gnupg
- wget
```

**Default value for installation_packages:**
```yaml
- libdbd-mysql
- libdbd-mysql-perl
- libcpan-meta-yaml-perl
- libjson-perl
- libdevice-serialport-perl
- libyaml-appconfig-perl
- cpanminus
- libmodule-pluggable-perl
- libcrypt-rijndael-perl
- libxml-simple-perl
- usbutils
- fhem
```

## Dependencies

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- name: Execute tasks on servers
  hosts: fhem
  roles:
    - role: zephyr82.fhem.installation
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
