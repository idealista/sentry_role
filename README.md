![Logo](logo.gif)

[![Build Status](https://travis-ci.org/idealista/sentry_role.png)](https://travis-ci.org/idealista/sentry_role)

Sentry Ansible role
=========

This role installs a Sentry server

- [Getting Started](#getting-started)
	- [Prerequisites](#prerequisites)
	- [Installing](#installing)
- [Usage](#usage)
- [Testing](#testing)
- [Built With](#built-with)
- [Versioning](#versioning)
- [Authors](#authors)
- [License](#license)
- [Contributing](#contributing)

## Getting started

Install Sentry in a Debian system

### Prerequesites

Sentry needs Redis and PostgreSQL for working. This role only install and setup Sentry, so you will need other roles to accomplish Sentry dependencies.
These other roles can be helpful:
```
idealista.redis_role
idealista.postgresql_role 
```

### Installing

Create or add to your roles dependency file (e.g requirements.yml):

``` yml
- src: idealista.sentry_role
  version: 1.0.0
  name: sentry
```

Install the role with ansible-galaxy command:

```
ansible-galaxy install -p roles -r requirements.yml -f
```

Use in a playbook:

```
- hosts: someserver
  roles:
    - role: sentry
```

## Usage

Variables explanation:

- `sentry_version` Sentry version to install
- `sentry_webserver.listen_ip` the local ip where Sentry listen to requests 
- `sentry_webserver.listen_port` the local port where Sentry listen to request
- `sentry_environment` https://docs.sentry.io/enriching-error-data/environments/
- `sentry_configuration_path` path to store configuration files
- `sentry_installation_path` path to install sentry
- `sentry_filestore_path` file store path
- `sentry_configuration_templates` list of sentry configuration templates
- `sentry_user` Sentry user
- `sentry_group` Sentry group
- `sentry_admin_email` admin email for Sentry notifications
- `sentry_admin_users` list of admin users in Sentry. For example:
```
  - email: 'someuser@email'
    password: 'somepassword'
    superuser: yes
```
- `sentry_secret_key` a secret key used for session signing
- `sentry_allow_users_create_accounts` should Sentry allow users to create new accounts?
- `sentry_beacon_enabled`: https://docs.sentry.io/server/beacon/
- `sentry_cleanup_keep_days` number of days to keep data

Cron format to set cleaning task up

- `sentry_cleanup_cron.minute`
- `sentry_cleanup_cron.hour`
- `sentry_cleanup_cron.day`
- `sentry_cleanup_cron.month`
- `sentry_cleanup_cron.weekday`

PostgreSQL connection variables:

- `sentry_postgresql_database.user`
- `sentry_postgresql_database.password`
- `sentry_postgresql_database.host`
- `sentry_postgresql_database.port`

Redis connection variables:

- `sentry_redis_database.host`
- `sentry_redis_database.port`

External SMTP configuration variables:

- `sentry_smtp_enabled`: enable external smtp notifications

If external SMTP is enabled, following variables must be defined

- `sentry_smtp_config.mail_from`
- `sentry_smtp_config.user`
- `sentry_smtp_config.password`
- `sentry_smtp_config.tls_enabled`
- `sentry_smtp_config.host`
- `sentry_smtp_config.port`

## Testing

Tests are executed with Molecule and Docker

Run `pip install requirements-test.txt` before running tests to install dependencies

Launch tests:

`molecule test`

## Built With

![Ansible](https://img.shields.io/badge/ansible-2.8.2-green.svg)

## Versioning

For the versions available, see the [tags on this repository](https://github.com/idealista/sentry_role/tags).

Additionaly you can see what change in each version in the [CHANGELOG.md](CHANGELOG.md) file.

## Authors

* **Idealista** - *Work with* - [idealista](https://github.com/idealista)

See also the list of [contributors](https://github.com/idealista/sentry_role/contributors) who participated in this project.

## License

![Apache 2.0 License](https://img.shields.io/hexpm/l/plug.svg)

This project is licensed under the [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0) license - see the [LICENSE](LICENSE) file for details.

## Contributing

Please read [CONTRIBUTING.md](.github/CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests to us.


