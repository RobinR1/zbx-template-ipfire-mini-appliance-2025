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
