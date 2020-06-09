# NetBox Registration
[Official document](https://netbox.readthedocs.io/en/stable/)

## Verified with
- ansible 2.9.7
- python 3.8.2

## What we can do
Registration of
- Sites
  - `--tags=site`
- Manufacturers
  - `--tags=manufacturer`
- Device Roles
  - `--tags=device_role`
- Device Types
  - `--tags=device_type`

Registration and modify of
- Devices
  - `--tags=device`
  - `--tags=device_only`
- Device の Management interface
  - `--tags=device`
  - `--tags=device_interface`
- IP address
  - `--tags=device`
  - `--tags=ipam`
- Device の Primary IP
  - `--tags=device`
  - `--tags=ipam`

## Preparation
### Installation
Install [pynetbox](https://github.com/digitalocean/pynetbox) and [Collection module](https://galaxy.ansible.com/fragmentedpacket/netbox_modules)
```
pip install pynetbox
ansible-galaxy collection install fragmentedpacket.netbox_modules
```

### host_vars
Add the following to `host_vars/my-netbox.yml`  
- URL of NetBox
- [Token for connecting to NetBox API](https://netbox.readthedocs.io/en/stable/api/authentication/#tokens)

### Items to register
Add the items to the CSV file in `file/` directory (see `files/sample.csv`). 
Specify the CSV file with `--extra-vars` when executing command.


## Commands
If no tag is specified, all items will be registered.

### New registration of Sites, Manufacturers, Device Roles, Device Types

```
ansible-playbook netbox_registration.yml --diff --tags=site
ansible-playbook netbox_registration.yml --diff --tags=manufacturer
ansible-playbook netbox_registration.yml --diff --tags=device_role
ansible-playbook netbox_registration.yml --diff --tags=device_type
```

### New registration or modification of Device
Specify the CSV file for registering Devices by using `--extra-vars device_csv=`. 
If no file is specified, `files/sample.csv` will be used.
```
ansible-playbook netbox_registration.yml --diff --tags=device --extra-vars device_csv=files/sample.csv
```

### New registration or modification to IPAM
Specify the CSV file for registering Devices by using `--extra-vars device_csv=`. 
If no file is specified, `files/sample.csv` will be used.
```
ansible-playbook netbox_registration.yml --diff --tags=ipam --extra-vars device_csv=files/sample.csv
```
