Promtail  Role
=========

This role installs promtail on a host as local agent or docker container to collect logs and send them to Loki.

It comes with basic configuration :

- Promtail user and group are created
- Promtail user added to the docker group and logs-reader
- Promtail configuration file is created to send basic logs to Loki :
  - **syslog** : `/var/log/syslog`
  - **Basic system logs** : `/var/log/*.log`
  - **lastlog** : `/var/log/lastlog`
  - **Docker logs** : through promtail **scrape_configs** `docker_sd_configs`

Requirements
------------

- [Ansible](https://www.ansible.com/) - Ansible must be installed to execute the playbook.
- [Docker](https://www.docker.com/) - Docker must be installed to run promtail as a container.
- [Loki](https://grafana.com/oss/loki/) - Loki must be installed to another server and accessible to promtail.

Role Variables
--------------

| Variable | Description | Default |
|----------|-------------|---------|
| `promtail_loki_url` | URL of the Loki server | None |
| `promtail_port` | Port of the Promtail server | `3101` |
| `promtail_log_reader_group` | Group to add the promtail user to read logs | `adm` |

Dependencies
------------

None.

Example Playbook
----------------

File `inventory/hosts_vars/host` for server example :

```yaml
promtail_loki_url: http://<loki_server>:3100
```

Playbook example : 
```
- hosts: servers
  roles:
    - promtail
```

License
-------

BSD
