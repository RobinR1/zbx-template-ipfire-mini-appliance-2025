# IPFire Mini Appliance 2025 by Zabbix Agent Active

## Description

This template gathers statistics for the [IPFire Mini R2 Appliance (2025)](https://www.ipfire.org/docs/hardware/lightningwirelabs/mini-r2).

## Overview

For Zabbix version: 7.4

Supports monitoring of:
* BIOS version/vendor/revision/release date
* CPU temperature

Use in conjunction with a default Template OS Linux-template for 
CPU/Memory/Storage monitoring of the IPFire appliance/instance.

This template was created for:

- IPFire Mini R2 Appliance (2025) - 2nd generation

**Warning**: This template will *NOT* work on the 1st generation IPFire Mini 
Appliance (2019) or any other IPFire appliance.

## Author

Robin Roevens

## Setup

- Install and configure [IPFire addon `zabbix_agentd`](https://www.ipfire.org/docs/addons/zabbix_agentd)
  using Pakfire.
- Login to the IPFire Mini appliance SSH console
    - Create a new config file for the zabbix_agentd userparameters:
      ```bash
      vi /etc/zabbix_agentd/zabbix_agentd.d/template_ipfire_mini_appliance_2025.conf
      ```
    - Paste the following content into the file (`i` to enter insert mode in Vi):
      ```ini
      UserParameter=ipfire_appliance_v2.firmware.info,sudo /usr/sbin/dmidecode -t 0 | awk -F': ' '/^\t(Vendor|Version|Release Date|BIOS Revision):/{gsub(/^\t/,"");v[$1]=$2}END{printf "{\"Vendor\":\"%s\",\"Version\":\"%s\",\"Release Date\":\"%s\",\"BIOS Revision\":\"%s\"}\n",v["Vendor"],v["Version"],v["Release Date"],v["BIOS Revision"]}'
      ```
    - Save the file and exit the editor (`:wq`).
    - Edit the sudoers file for the zabbix_agentd user to allow running dmidecode without a password:
      ```bash
      visudo -f /etc/sudoers.d/zabbix_agentd_user
      ```
    - Add the following line (`i` to enter insert mode in Vi):
      ```
      zabbix ALL=(ALL) NOPASSWD: /usr/sbin/dmidecode -t 0
      ```
    - Save the file and exit the editor (`:wq`).

## Zabbix configuration

No specific Zabbix configuration is required.

### Macros used
|Name|Description|Default|
|----|-----------|-------|
|{$CPU.TEMP.WARN} |<p>CPU temperature warning threshold</p>|`70` |
|{$CPU.TEMP.CRIT} |<p>CPU temperature critical threshold</p>|`105` |

## Credits

[IPFire Team](https://www.ipfire.org) for the IPFire distro and for accepting my 
contributions to allow easier/better monitoring using Zabbix Agent.

## Feedback

Please report any issues with the template at https://github.com/RobinR1/zbx-template-ipfire-mini-appliance-2025/issues
