![Ansible Lint](https://github.com/johanneskastl/ansible-role-simple_firewalld_configuration/workflows/Ansible%20Lint/badge.svg)

simple_firewalld_configuration
=========

Simple configuration for firewalld, only ports and services allowed/disallowed

Requirements
------------

Firewalld should be installed and running. This role does not take care of installing, enabling or starting firewalld.

Role Variables
--------------

In case you want to allow traffic to your machine, you can use pre-defined service names or specify the exact details (which port? which protocol?.

- `firewalld_services_enabled`: (list) firewalld knows many services by name (e.g. `ssh` or `http`), so you can use those names to allow the connection. The role expects a list of service names in this variable.
- `firewalld_ports_enabled`: (list) if there is no well-known service that describes the port you want to open, you can use this variable to define it. It needs to be a list of strings in `port/protocol` syntax, i.e. `53/tcp` or `80/tcp` or `123/udp` or similar.

In case you want to make sure that a connection is not allowed, you can use the variables `firewalld_services_disabled` or `firewalld_ports_disabled` to disable the rule. They behave exactly the same as the variables that allow the ports, e.i. `firewalld_services_disabled` expects a list of service names while `firewalld_ports_disabled` wants a list of `port/protocol` strings...

Dependencies
------------

None.

Example Playbook that allows SSH as well as TCP/UDP on port 53
----------------

    - hosts: servers
      roles:
        - role: 'johanneskastl.simple_firewalld_configuration'
          firewalld_ports_enabled:
            - '53/tcp'
            - '53/udp'
          firewalld_services_enabled:
            - 'ssh'

License
-------

BSD-3-Clause

Author Information
------------------

I am Johannes Kastl, reachable via kastl@b1-systems.de.
