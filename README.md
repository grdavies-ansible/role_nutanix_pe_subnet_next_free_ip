# Nutanix Role to deploy Prism Central

This Ansible role get the list of available IP addresses from an AHV IPAM enabled subnet and attempts to provide the first free IP address from that range.

## Requirements

The following collection need to be installed as they are used within this role;
- nutanix.ncp

## Role Variables

| Variable                                    | Required | Default         | Choices                                                                         | Comments                                                                                                                                                                                                                          |
|---------------------------------------------|----------|-----------------|---------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| nutanix_host                                | yes      |                 |                                                                                 | The IP address or FQDN for the Prism (Element only) to which you want to connect.                                                                                                                                                 |
| nutanix_username                            | yes      |                 |                                                                                 | A valid username with appropriate rights to access the Nutanix API.                                                                                                                                                               |
| nutanix_password                            | yes      |                 |                                                                                 | A valid password for the supplied username.                                                                                                                                                                                       |
| nutanix_port                                | no       | 9440            |                                                                                 | The Prism TCP port.                                                                                                                                                                                                               |
| validate_certs                              | no       | no              | yes | no                                                                        | Whether to check if Prism UI certificates are valid.                                                                                                                                                                              |
| nutanix_next_ip_subnet_name                 | yes      |                 |                                                                                 | The name of the AHV IPAM enabled subnet upon which to search for an available IP address                                                                                                                                          |
| nutanix_next_ip_ping_test                   | no       | no              | yes | no                                                                        | Whether to perform an ICMP test of the IP returned by AHV IP to verify that it is available.                                                                                                                                      |

### Returned Variables

| Variable                                    | Comments                                                                                                                                                                                                                          |
|---------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| nutanix_subnet_ipam_next_available_ip       | The next unallocated IP address from the AVH IPAM pool.                                                                                                                                                                           |


## Example Playbook

```
- hosts: localhost
  gather_facts: false
  roles:
    - role: grdavies.role_nutanix_pe_subnet_next_free_ip
  vars:
    nutanix_host: "10.42.70.37"
    nutanix_username: admin
    nutanix_password: nx2Tech075!
    nutanix_debug: False
    nutanix_next_ip_subnet_name: Primary
    nutanix_next_ip_ping_test: yes
```


## License

See LICENSE.md

## Author Information

Ross Davies
