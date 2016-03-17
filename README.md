Role Name
=========

Installation and basic configuration of an ufw-firewall

Requirements
------------

Role Variables
--------------

- **ufw_whitelisted_addresses_extra**: list of ip addresses whitelisted for all ports
- **ufw_whitelisted_out_ports_extra**: list of whitelisted outgoing ports
    
```    
    ufw_whitelisted_out_ports_extra:
           - { to_port: 22, proto: 'tcp', to_ip: '192.168.1.1' }
```

- **ufw_whitelisted_in_ports_extra**: list of whitelisted incoming ports

```    
    ufw_whitelisted_in_ports_extra:
           - { to_port: 22, proto: 'tcp', from_ip: '192.168.1.1' }
```

- **ufw_persistent**: Make rules persistent after reboot (/!\ be careful)

- **ufw_logging**: logging mode on rejection. Available mode:
    - on
    - off
    - low
    - medium
    - high
    - full

Dependencies
------------

Example Playbook
----------------

    - hosts: servers
      roles:
        - { role: steamroles-interne/ufw-firewall, tags: [ firewall ] }


Ad-hoc command to see rules : 

ansible all -a "/usr/sbin/ufw status verbose" -i hosts/all -u steamulo --sudo

License
-------


Author Information
------------------

STEAMULO - http://www.steamulo.com
