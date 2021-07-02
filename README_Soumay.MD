
## Ansible Training Homework ##

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Initial steps for setting up the lab ###

1. Setup environment variables in a file for Ansible & Lab utilization.
2. Created inventory for tower setup.
3. Connected workstation and control node for OSP inventory.
4. Modified password in tower_cli.cfg 
5. Modified path of key in (-e) preconfig 
6. post config - removed first line or blank module - added tower ssl verify as NO
7 variable- {{ path_to_opentlc_key }} for openstack.pem
8. Resolved error in  Job template for OSP Instances
9. Created a project in ansible tower for job_template task 

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Playbook Creation for LAB ###


__Edited two roles and one playbook for achieving the same.__

1. site-smoke-osp.yml - For smoke testing the functionality of the playbook
2. Role - osp-servers - To generate the required infra for testing
3. Role - osp-instance-delete & site-osp-delete.yaml - To delete the generated infra after achieving the desired task.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
***Playbook - site-osp-instances.yml & Role - osp-servers***
**Variables Utilized**
```
*Server Details*
osp_servers:
  frontend:
    name: frontend
    state: present
    cloud: openstack
    image: rhel-guest
    key_name: ansible_ssh
    flavor: m1.medium
    security_group: frontend
    meta:
      - { group: frontends, deployment_name: QA}
  app1:
    name: app1
    state: present
    image: rhel-guest
    cloud: openstack
    key_name: ansible_ssh
    flavor: m1.medium
    security_group: apps
    meta:
      - { group: apps, deployment_name: QA}
  app2:
    name: app2
    state: present
    image: rhel-guest
    cloud: openstack
    key_name: ansible_ssh
    flavor: m1.medium
    security_group: apps
    meta:
      - { group: apps, deployment_name: QA}
  db:
    name: db
    state: present
    cloud: openstack
    image: rhel-guest
    key_name: ansible_ssh
    flavor: m1.medium
    security_group: db
    meta:
      - { group: appdbs, deployment_name: QA}

*Network Values*
osp_networks:
 
 *External Network Details*
  external:
    cloud: openstack
    name: ext_network
    external: true
    admin_state_up: no
    provider_network_type: flat
    provider_physical_network: datacenter
*Internal Network Details*
  internal:
    cloud: openstack
    name: int_network
    external: false
    admin_state_up: yes
    provider_network_type: null
    provider_physical_network: null


*Subnet Values*
osp_subnets:
*Internal Subnet Details*
  internal:
    cloud: openstack
    name: int_subnet
    network_name: int_network
    cidr: 172.16.0.0/24
    ip_version: 4
    gateway_ip: null
    enable_dhcp: yes
    allocation_pool_start: null
    allocation_pool_end: null
    
*External Subnet Details*
  external:
    cloud: openstack
    name: ext_subnet
    network_name: ext_network
    cidr: 192.0.2.0/24
    ip_version: 4
    gateway_ip: 192.0.2.254
    enable_dhcp: no
    allocation_pool_start: 192.0.2.150
    allocation_pool_end: 192.0.2.200

*Router Details*
osp_router_cloud: openstack
osp_router_name: router
osp_router_network: ext_network

*Security Group & Rules*
osp_securitygroup:
  #Rules for apps instances
  apps:
    security_group: apps
    cloud: openstack
  
*Rules for frontend instance*
  frontend:
    security_group: frontend
    cloud: openstack

*Rules for db instances*
  db:
    security_group: db
    cloud: openstack
remote_ip_prefix: 0.0.0.0/0

*Flavour Details*
osp_flavour:
  cloud: openstack
  size: m1.medium
  ram: 2048
  vcpus: 1
  disk: 20
```
