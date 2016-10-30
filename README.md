Role Name
=========

Simple ansible role to install and config xinetd to proxy connections

Requirements
------------

Supports Red Hat and Debian based distros

Role Variables
--------------

1. `xinetd_proxy_config_path` defaults to `/etc/xinetd.d`
2. `xinetd_proxy_cleanup` defaults to `false`

If cleanup is set to true the role removes various default services that are included in OS packages.

To define the services you will need to use a dict called `xinetd_proxy_services`. An example to proxy a connection to your router's admin interface via a VPN is included below:

```yaml
xinetd_proxy_services:
  - name: router
    disable: 'no'
    socket_type: stream
    protocol: tcp
    wait: 'no'
    only_from: "10.0.1.0/16"
    user: nobody
    listen_address: "{{ ansible_tun0.ipv4.address }}"
    listen_port: 80
    target_address: "{{ ansible_default_ipv4.gateway }}"
    target_port: 80
```

Dependencies
------------

None

Example Playbook
----------------

License
-------

GPL3

Author Information
------------------

Tim Fletcher
