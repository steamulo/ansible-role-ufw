ANSIBLE-ROLE-UFW
=========

Installation and basic configuration of ufw on the target machine.

The role checks the current configuration of ufw if and applies the modifications provided by the playbook.

Role Variables
--------------

- **ufw_whitelisted_addresses** and **ufw_whitelisted_addresses_extra**: list of IP addresses or ranges whitelisted for all ports.

```yaml
ufw_whitelisted_addresses_extra:
   - 1.1.1.1
   - 1.0.0.0/8
```


- **ufw_whitelisted_out_ports** and **ufw_whitelisted_out_ports_extra**: list of whitelisted outgoing ports.
If you want to open a port to any IP address (oftenly 80 and 443 for public web services) you can omit the
attribute *to_ip*.
    
```yaml
ufw_whitelisted_out_ports_extra:
   - { to_port: 22, proto: 'tcp', to_ip: '192.168.1.1' }
   - { to_port: 80, proto: 'tcp' }
   - { to_port: 443, proto: 'tcp' }
```

- **ufw_whitelisted_in_ports** **ufw_whitelisted_in_ports_extra**: list of whitelisted incoming ports. See the documentation of
the _ufw_whitelisted_out_ports_ variable for details.

```yaml
ufw_whitelisted_in_ports_extra:
    - { to_port: 22, proto: 'tcp', from_ip: '192.168.1.1' }
    - { to_port: 80, proto: 'tcp' }
    - { to_port: 443, proto: 'tcp' }
```

- **ufw_logging**: logging mode on rejection. Available modes:
    - on
    - off
    - low
    - medium
    - high
    - full
 
` **advanced_ufw_before_rules**

Dependencies
------------

Example Playbook
----------------

```yaml
- hosts: servers
  roles:
    - { role: steamulo.ufw, tags: [ firewall ] }
  vars:
    ufw_whitelist_in_ports_extra:
      - { to_port: 22, proto: 'tcp', from_ip: '192.168.1.1' }
```

Ad-hoc command to see rules: 

`ansible all -a "sudo /usr/sbin/ufw status verbose" -i hosts/all -u steamulo`

License
-------


Author Information
------------------

STEAMULO - http://www.steamulo.com
