# Ansible Role: centreon-database

Installs centreon-database (MariaDB server)

## Supported platforms

```
CentOS 7
```

## Post install

- include: config.yml
- include: mysql_secure_installation.yml

## Requirements

Dépots accessible

## Role Variables

MariaDB version:

```
mariadb_version: 10.5.x

## Dependencies
roles:
  - common-packages
  - disable-selinux-firewalld

## Example Playbook

```
    - hosts: servers
      roles:
        - { role: centreon-database }
```

## Credits

- [Attila van der Velde](https://github.com/vdvm)

