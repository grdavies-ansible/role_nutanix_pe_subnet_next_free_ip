# Nutanix Role to deploy Prism Central

This Ansible role get the list of available IP addresses from an AHV IPAM enabled subnet and attempts to provide the first free IP address from that range.

## Requirements

- grdavies.role_nutanix_prism_api
- nutanix.ncp

## Input Variables

| Variable                                                | Required | Default         | Choices                                                                         | Comments                                                                                                                                                                                                                          |
|---------------------------------------------------------|----------|-----------------|---------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| role_nutanix_pe_subnet_next_free_ip_host                | yes      |                 |                                                                                 | The IP address or FQDN for the Prism (Element only) to which you want to connect.                                                                                                                                                 |
| role_nutanix_pe_subnet_next_free_ip_host_username       | yes      |                 |                                                                                 | A valid username with appropriate rights to access the Nutanix API.                                                                                                                                                               |
| role_nutanix_pe_subnet_next_free_ip_host_password       | yes      |                 |                                                                                 | A valid password for the supplied username.                                                                                                                                                                                       |
| role_nutanix_pe_subnet_next_free_ip_host_port           | no       | 9440            |                                                                                 | The Prism TCP port.                                                                                                                                                                                                               |
| role_nutanix_pe_subnet_next_free_ip_host_validate_certs | false    | false           | true / false                                                                    | Whether to check if Prism UI certificates are valid.                                                                                                                                                                              |
| role_nutanix_pe_subnet_next_free_ip_debug               | false    | false           | true / false                                                                    | Enable debug logging.                                                                                                                                                                                                             |
| role_nutanix_pe_subnet_next_free_ip_subnet_name         | yes      |                 |                                                                                 | The name of the AHV IPAM enabled subnet upon which to search for an available IP address                                                                                                                                          |
| role_nutanix_pe_subnet_next_free_ip_ping_test           | no       | false           | true / false                                                                    | Whether to perform an ICMP test of the IP returned by AHV IP to verify that it is available.                                                                                                                                      |

### Returned Variables

| Variable                                    | Comments                                                                                                                                                                                                                          |
|---------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| role_nutanix_pe_subnet_next_free_ip       | The next unallocated IP address from the AVH IPAM pool.                                                                                                                                                                           |

## Example Playbook

```YAML
- hosts: localhost
  gather_facts: false
  roles:
    - role: grdavies.role_nutanix_pe_subnet_next_free_ip
  vars:
    role_nutanix_pe_subnet_next_free_ip_host: "10.42.70.37"
    role_nutanix_pe_subnet_next_free_ip_host_username: admin
    role_nutanix_pe_subnet_next_free_ip_host_password: nx2Tech075!
    role_nutanix_pe_subnet_next_free_ip_debug: False
    role_nutanix_pe_subnet_next_free_ip_subnet_name: Primary
    role_nutanix_pe_subnet_next_free_ip_ping_test: yes
```

## License

See LICENSE.md

## Author Information

Ross Davies
