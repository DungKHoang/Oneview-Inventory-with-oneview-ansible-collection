## OneView Resources Inventory 

This series of Ansible playbooks perform an inventory of resources managed by OneView including:
   * ProLiant Blade servers
   * Synergy enclosures
   * Synergy frame managers
   * Synergy device bays
   * Synergy fan devices
   * Synergy PDU devices
   * Synergy interconnect bays
   * Synergy appliances

Ansible playbooks will generate CSV files as output from the inventory and CSV files can be used to import into ServiceNow to populate CMDB data. As a result, some CSV headers may contain text that are specific to ServiceNow CMDB CI attributes.


## Configuration
Use the OneView Ansible github(https://github.com/HewlettPackard/oneview-ansible-collection) to configure the environment 


## OneView config file
The playbook requires a oneview-config.csv that contains OneView FQDN/IP address and OneView credentials. Here is an example of config:
````
ip,username,password,authLoginDomain,api_version
10.1.10.232,administrator,password,local,4600
10.1.10.237,administrator,password,local,4600
````

## Workflow
The flow for playbooks is as follow:
* oneview-inventory.yml --> oneview-inventory-tasks.yml 

                           |---> server-hardware-sub-inventory.yml

                           |---> enclosure-inventory.yml

* server-hardware-sub-inventory.yml

   |---> adapter-sub-inventory.yml

         |---> physical-port-sub-inventory.yml

               |---> virtual-port-sub-inventory.yml

* enclosure-inventory.yml

   |---> enclosure-appliance-bay-inventory.yml

   |---> enclosure-device-bay-inventory.yml

   |---> enclosure-manager-bay-inventory.yml

   |---> enclosure-fan-bay-inventory.yml

   |---> enclosure-power-supply-bay-inventory.yml

   |---> enclosure-interconnect-bay-inventory.yml


## To run playbook
````
ansible-playbook oneview-inventory.yml --extra-vars "oneview_config_csv=oneview-config.csv" 
````

Enjoy!



