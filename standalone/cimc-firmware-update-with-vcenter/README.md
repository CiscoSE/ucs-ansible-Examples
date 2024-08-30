# Upgrading UCS Firmware for VCenter Based ESXi systems

## Overview
This is a demonstration tool showing how to upgrade UCS Firmware using Ansible to put each host in maintenance mode, then trigger a firmware update. If the system completes the firmware in the expected time period, the system is removed from maintenance mode. 

Key elements:
    - Only one host is completed at a time as written to avoid failures that impact systems that didn't experience errors. 
    - This is intended to be a demonstration script only with limited error checking or validation.
    - Currently only supports the XML API, but the Redfish API will be an option in the future.
    - Only intended for stand alone C series servers
    - The J2 file used to template the XML call to the XML API likely still requires some optimization depending on how you intend to map to the upgrade media.
    - The script, as written, was intended for use with http, sourced local to the server being upgraded. Upgrading over a WAN link will likely cause the firmware update to fail or require changes to the portion of the automation tracking the status of the ESXi returning to service. The http method is the fastest method available for this purpose.

## Running the script.

For testing purposes two environment variables were used with this script:

    VCENTER_PASSWORD    Contains the password for the vcenter account referenced in the ini file vcenter_user variable
    CIMC_PASSWORD       Contains the password for the CIMC account referenced in the ini file cimc_user variable

Both variables are required for this script to function as written:

```
    export VCENTER_PASSWORD='SomePasswordForVCenter'
    export CIMC_PASSWORD='SomePasswordForCIMC'
```

The following are common variables you should consider modifying before running the script:

- cimc_logon_name   Should contain the user name to logon to the CIMC
- vcenter_hostname  The FQDN or IP to connect (assuming DNS resolution is available on the host)
- vcenter_user      The user name to logon to vCenter (such as adminstrator@vsphere.local)
- huu_iso_host      The IP address of FQDN of the system hosting the ISO
- huu_remoteShare   The full path to the file including the file name

The following components were tested as part of this process:

    Installed with pip3

    ansible             9.2.0
    Jinja2              3.1.2
    lxml                5.3.0
    xmljson             0.2.1

    Installed with ansible-galaxy

    community.vmware    4.1.0
    ansible.utils       2.12.0

    Note: I had to force reinstall of ansible.utils to get the ansible.utils.from_xml filter to function properly.

To run the script:

```
    ansible-playbook upgrade-firmware.yaml
```


