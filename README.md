ANSIBLE-ROLE-UFW
=========

Installation and basic configuration of a UFW on the target machine.
The role checks the current configuration of the UFW if one exists and apply the modifications provided by the playbook.

Role Variables
--------------

- **ufw_whitelisted_addresses_extra**: list of ip addresses whitelisted for all ports with the possibility to specify a mask. 
Please specify the first IP address of the range if you specify a mask different from 32
```    
    ufw_whitelisted_addresses_extra:
           - 1.1.1.1
           - 1.0.0.0/8
```


- **ufw_whitelisted_out_ports_extra**: list of whitelisted outgoing ports. If you want to open a port to any IP address (for example 80 or 443 ) you can 
omit the attribute *to_ip*
    
```    
    ufw_whitelisted_out_ports_extra:
           - { to_port: 22, proto: 'tcp', to_ip: '192.168.1.1' }
           - { to_port: 80, proto: 'tcp' }
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
