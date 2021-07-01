
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

_1. site-smoke-osp.yml - For smoke testing the functionality of the playbook_
_2. Role - osp-servers - To generate the required infra for testing_
_3. osp-instance-delete - To delete the generated infra after achieving the desired task._

**Variables Utilized**
Playbook Name - site-osp-instances.yml
Role Name - osp-servers

Network   | External 
--------    --------
    cloud |openstack
    name  |ext_network
  external|true
admin_state_up: no
    provider_network_type: flat
    provider_physical_network: datacenter
