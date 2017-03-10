# Ansible Role: keepalived

Installs and configures keepalived.

## Requirements

None.

## Role Variables

### `defaults/main.yml`

* `keepalived_global: []`
* `keepalived_vrrp_sync_groups: []`
* `keepalived_vrrp_scripts: []`
* `keepalived_vrrp_instances: []`

### `vars/main.yml`
The full example of all options.

## Dependencies

None.

## Example Playbook

    - hosts: servers
      roles:
         - role: keepalived
           keepalived_global:
             router_id: "DEVEL"
           keepalived_vrrp_sync_groups:
             haproxy:
               instances:
                 - external
           keepalived_vrrp_scripts:
             check_haproxy:
               check_script: "killall -0 haproxy"
               interval: 2
               weight: 2
           keepalived_vrrp_instances:
             external:
               interface: "eth0"
               state: MASTER
               virtual_router_id: 10
               priority: 100
               advert_int: 1
               auth_pass: "password"
               vips:
                 - "{{ ansible_default_ipv4.address }}"
               track_scripts:
                 - check_haproxy
               raw_config:
                 - 'mcast_src_ip @IP'

## Author Information

z
