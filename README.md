Role Name
=========

Send logs from ansible host's filesystem to datadog.


Role Variables
--------------

Defaults:

`vector_user`: vector
`vector_version`: 0.30.0
`vector_checksum`: sha256:8333b148711c08a957c2a4133ff095de2790d1eccc9437c06a72a5d9ac11615a
`vector_enable_api`: yes

`vector_config_*`: None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: vector }

Example `vector_config_*` settings:

```yaml
--- # Webservers config
vector_config_web:
  sources:
    - name: apache
      files:
        - /var/log/httpd/www.site.com*.log
      service: "httpd"

--- # Database config
vector_config_dbs:
  sources:
    - name: slow-log
      files:
        -  /var/log/mysql/mysql-slow.log
      service: "mysql"
```

Webservers will send their apache logs, databases will send their slow log. If
for some reason you're running a server as a database and a webserver, the
settings will get merged and both sets of logs will be shipped to datadog.

All variables starting with `vector_config_` are merged together to generate a
complete config.
