# zephyr82.fhem config_dblog Role

The role configures the DbLog configuration for using a database like MariaDB, MySQL and so on for logging data comfing from FHEM. 

## Requirements

A working FHEM installation

## Role Variables

There are some constraints on which keys in the variable `config_dblog_db_config` could be set. E. g. the keys `host` and `socket` are mutually exclusive.

| Variable                  | Type | Required | Default (defaults/main.yml)     | Description                                                  |
|---------------------------|------|----------|---------------------------------|--------------------------------------------------------------|
| config_dblog_db_conf_path | str  | yes      | /opt/fhem/contrib/dblog/db.conf | Path to the dblog database configuration file.               |
| config_dblog_conf_owner   | str  | yes      | fhem                            | Owner of the dblog database configuration file.              |
| config_dblog_conf_group   | str  | yes      | dialout                         | Group of the dblog database configuration file.              |
| config_dblog_conf_mode    | str  | yes      | 0644                            | Mode of the dblog database configuration file.               |
| config_dblog_db_config    | dict | yes      | (see below)                     | Dictionary containing the database configuration parameters. |

### Sub-keys of `config_dblog_db_config`

| Key         | Type | Required | Default      | Choices / Constraint               | Description                                                      |
|-------------|------|----------|--------------|------------------------------------|------------------------------------------------------------------|
| type        | str  | yes      | mariadb      | mariadb, mysql, postgresql, sqlite | Type of the database.                                            |
| user        | str  | no       | fhem         | —                                  | Database username. Only used for MySQL, MariaDB, and PostgreSQL. |
| password    | str  | no       | fhempassword | —                                  | Database password. Only used for MySQL, MariaDB, and PostgreSQL. |
| database    | str  | no       | fhem         | —                                  | Database name; for SQLite this is the path to the database file. |
| host        | str  | no       | localhost    | mutually exclusive with socket     | Database host. Only used for MySQL, MariaDB, and PostgreSQL.     |
| socket      | str  | no       | ""           | mutually exclusive with host       | Database socket. Only used for MySQL and MariaDB.                |
| port        | int  | no       | 3306         | —                                  | Database port. Only used for MySQL, MariaDB, and PostgreSQL.     |
| utf8        | bool | no       | false        | —                                  | Whether to use UTF-8 encoding. Only used for MySQL.              |
| compression | bool | no       | false        | —                                  | Whether to use compression. Only used for MySQL and MariaDB.     |


## Dependencies

none

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- name: Configure database logging for FHEM via moduel DbLog
  hosts: FHEM
  vars:
    config_dblog_db_conf_path: "/opt/fhem/contrib/dblog/db.conf"
    config_dblog_db_config:
      type: "mariadb"
      user: "fhem"
      password: "fhempassword"
      database: "fhem"
      host: "localhost"
  roles:
    - role: zephyr82.fhem.config_dblog
      tags:
        - fhem_config_dblog
```

Please set the tag `fhem_config_dblog` explicitly when running the role so the task for creating the database and database schema does not get executed. And set the tag `fhem_config_db_create` to get the database for FHEM DbLog created explicitly.

Do so by using `ansible-playbook --tags fhem_config_dblog fhem.yml`.

## Role Idempotency

Only when you decide to _not_ run the play with the task for creating the database.

## License

<!-- TO-DO: Update the license to the one you want to use (delete this line after setting the license) -->
BSD

## Author Information

Zephyr82: https://github.com/Zephyr82
