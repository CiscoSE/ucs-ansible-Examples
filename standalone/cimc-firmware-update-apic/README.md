# Upgrading Firmware on APICs
This Ansible script provides a fast easy method for upgrading the firmware on the APICs.

## Concept of Operation
This script generates an XML API call to the CIMC of the APIC directing it towards an ISO staged on a web server. This example only uses an open web server, but could be easily modified to incorporate authentication, which is supported by the API. The example only provides for HTTP connections from the CIMC to the web server.

The script will upgrade as many devices as it finds in the inventory, and it does not wait for completion of the firmware on the first device before moving on to the second device. The APIC will usually reboot within a minute or two of running this script. It is advisable to comment out all but one APIC when running this script.

The script today requires the password to be entered when the script is run using the -k switch for the ansible-playbook command. The admin password of the CIMC is used to authenticate.

## Running the Script
The following steps are recommended for running this script:

- Edit the inventory file APIC IP addresses (APIC1, APIC2 and APIC3 under APICS) and comment out all but one APIC with a # sign at the start of the line.
- Edit the firmware file name to match the file name on your web server (**firmware_file** variable)
- Edit the firmware IP to match your web server (**firmware_ip** variable)
- Edit the firmware path to match the directly for the firmware on the web server (**firmware_path** variable)

From the directory that contains the inventory, run the following command:

```
ansible-playbook -k Config-Firmware.yaml
```

The playbook is pointed to the inventory file by default, and will use the variables and APIC IPs that are active in the inventory.

## Prerequisites

The following components are recommended when running this script:

| Package Name | Tested Version |
| ------------ | -------------- |
| ansible | 11.3.0 |
| lxml | 5.3.1 |
| xmljson | 0.2.1 |

You can download these elements and their dependencies using the following command for air gapped installation:
```
pip3 download ansible lxml xmljson
```
