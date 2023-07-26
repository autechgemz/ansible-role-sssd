# Ansible Role: sssd

## Description

Manage System Security Services Daemon.

## Requirements

None

## Dependencies

None

## OS Platforms

- CentOS-7
- Rockylinux 8 or higher
- AlmaLinux 8 or higher
- Ubuntu-18.04 or higher

## Example Playbook

```
- hosts: all
  roles:
    - sssd
```

## Role Variables

### sssd_package_name: (string)

```
sssd_package_ensure: 'present'
```

### sssd_optional_package_ensure: (string)

```
sssd_optional_package_ensure: 'present'
```

### sssd_service_ensure: (string)

```
sssd_service_ensure: 'started'
```

### sssd_service_enable: (bool)

```
sssd_service_enable: true
```

### sssd_optional_service_ensure: (string)

```
sssd_optional_service_ensure: 'started'
```

### sssd_optional_service_enable: (bool)

```
sssd_optional_service_enable: true
```

### sssd_authconfig_command: (list)

```
sssd_authconfig_command: []
```

### sssd_mkhomedir_command: (list)

```
sssd_mkhomedir_command:
  - 'pam-auth-update'
  - '--enable'
  - 'mkhomedir'
```

### sssd_config_options: (dict)

```
sssd_config_options: {}
```

## Example vars

```
sssd_config_options:
  sssd:
    debug_level: 2
    config_file_version: 2
    services: 'nss, pam, ssh, sudo'
    domains: default
  domain/default:
    id_provider: ldap
    auth_provider: ldap
    chpass_provider: ldap
    sudo_provider: ldap
    cache_credentials: true
    entry_cache_timeout: 1200
    override_homedir: /home/%u
    ldap_schema: rfc2307
    ldap_id_use_start_tls: true
    ldap_tls_reqcert: never
    ldap_search_timeout: 3
    ldap_network_timeout: 3
    ldap_opt_timeout: 3
    ldap_enumeration_search_timeout: 60
    ldap_enumeration_refresh_timeout: 300
    ldap_connection_expire_timeout: 600
    ldap_sudo_smart_refresh_interval: 600
    ldap_sudo_full_refresh_interval: 10800
    access_provider: ldap
    ldap_uri: ldaps://192.168.1.100:636
    ldap_search_base: dc=go,dc=home,dc=internal
    ldap_default_bind_dn: cn=ldapservice,ou=service_account,dc=go,dc=home,dc=internal
    ldap_access_filter: memberOf=cn=frontend,ou=groups,dc=go,dc=home,dc=internal
    ldap_sudo_search_base: ou=SUDOers,dc=go,dc=home,dc=internal
    ldap_user_search_base: ou=people,dc=go,dc=home,dc=internal
    ldap_group_search_base: ou=groups,dc=go,dc=home,dc=internal
    ldap_default_authtok_type: password
    ldap_default_authtok: openldap
  nss:
    homedir_substring: /home
    fallback_homedir: /home/%u
    entry_negative_timeout: 20
    entry_cache_nowait_percentage: 50
    shell_fallback: /bin/sh
    allowed_shells: /bin/sh /bin/bash /bin/zsh /bin/tcsh
  pam:
    offline_credentials_expiration: 2
    offline_failed_login_attempts: 3
    offline_failed_login_delay: 5
```
