---
title: oVirt 4.2.7 Release Notes
category: documentation
layout: toc
---

# oVirt 4.2.7 Release Notes

The oVirt Project is pleased to announce the availability of the 4.2.7 Second Release Candidate as of October 04, 2018.

oVirt is an open source alternative to VMware™ vSphere™, providing an
awesome KVM management interface for multi-node virtualization.
This release is available now for Red Hat Enterprise Linux 7.5,
CentOS Linux 7.5 (or similar).


To find out how to interact with oVirt developers and users and ask questions,
visit our [community page]"(/community/).
All issues or bugs should be reported via
[Red Hat Bugzilla](https://bugzilla.redhat.com/enter_bug.cgi?classification=oVirt).
The oVirt Project makes no guarantees as to its suitability or usefulness.
This pre-release should not to be used in production, and it is not feature
complete.


For a general overview of oVirt, read the [Quick Start Guide](/documentation/quickstart/quickstart-guide/)
and visit the [About oVirt](/documentation/introduction/about-ovirt/) page.

For detailed installation instructions, read the [Installation Guide](/documentation/install-guide/Installation_Guide/).

To learn about features introduced before 4.2.7, see the [release notes for previous versions](/documentation/#previous-release-notes).


## Install / Upgrade from previous versions

### CentOS / RHEL


## RELEASE CANDIDATE

In order to install this Release Candidate you will need to enable pre-release repository.




In order to install it on a clean system, you need to install


`# yum install `[`http://resources.ovirt.org/pub/yum-repo/ovirt-release42-pre.rpm`](http://resources.ovirt.org/pub/yum-repo/ovirt-release42-pre.rpm)


and then follow our
[Installation Guide](http://www.ovirt.org/documentation/install-guide/Installation_Guide/).



### No Fedora support

Regretfully, Fedora is not supported anymore, and RPMs for it are not provided.
These are still built for the master branch, so users that want to test them,
can use the [nightly snapshot](/develop/dev-process/install-nightly-snapshot/).
At this point, we only try to fix problems specific to Fedora if they affect
developers. For some of the work to be done to restore support for Fedora, see
also tracker [bug 1460625](https://bugzilla.redhat.com/showdependencytree.cgi?id=1460625&hide_resolved=0).

### oVirt Hosted Engine

If you're going to install oVirt as a Hosted Engine on a clean system please
follow [Hosted_Engine_Howto#Fresh_Install](/documentation/how-to/hosted-engine/#fresh-install)
guide or the corresponding section in
[Self Hosted Engine Guide](/documentation/self-hosted/Self-Hosted_Engine_Guide/).

If you're upgrading an existing Hosted Engine setup, please follow
[Hosted_Engine_Howto#Upgrade_Hosted_Engine](/documentation/how-to/hosted-engine/#upgrade-hosted-engine)
guide or the corresponding section within the
[Upgrade Guide](/documentation/upgrade-guide/upgrade-guide/).

### EPEL

TL;DR Don't enable all of EPEL on oVirt machines.

The ovirt-release package enables the EPEL repositories and includes several
specific packages that are required from there. It also enables and uses
the CentOS SIG repos, for other packages.

If you want to use other packages from EPEL, you should make sure to
use `includepkgs` and add only those you need avoiding to override
packages from other repos.

## What's New in 4.2.7?

### Enhancements

#### imgbased

 - [BZ 1613931](https://bugzilla.redhat.com/1613931) <b>[RFE] Add the ability to recover from failed upgrades</b><br>Feature: <br>The recover verb was added to imgbase<br><br>Reason: <br>imgbase creates LVs while upgrading ovirt-node-ng, if for any reason imgbase fails, and those LVs remain on the system, rerunning the upgrade fails on "existing LVs".<br><br>Result: <br>`imgbase --experimental recover` will try to find stale LVs that remained on the system due to a failed upgrade, and remove the.  imgbase will prompt the user before removing LVs, unless used with --force.

#### oVirt Engine

 - [BZ 1610979](https://bugzilla.redhat.com/1610979) <b>[downstream clone - 4.2.7] [RHEL-7.6] Limit east-west traffic of VMs with network filter</b><br>The new filter is called "clean-traffic-gateway" and can be chosen in vnic profiles. Then for every vm nic, with this vnic, the "GATEWAY_MAC" network filter parameter should be specified for the filter to work properly. Also for DHCP to be properly working, every vm nic using vnic with this filter, should specify another "GATEWAY_MAC" with value "ff:ff:ff:ff:ff:ff". Because DHCP is using broadcast MAC address in its requests.

#### VDSM

 - [BZ 1628477](https://bugzilla.redhat.com/1628477) <b>[downstream clone - 4.2.7] After importing KVM VM the actual size is bigger than the virtual size</b><br>Feature: <br><br>Added KVM Sparseness support to KVM to oVirt Virtual Machine Importing so that when Thin Provisioning is enabled, the Disk Size of the original KVM Image will be preserved after importing to oVirt.   <br><br>Reason: <br><br>Unless the user specifically specifies pre-allocation, the Disk Size of the Virtual Machine should be no larger than required during initial allocation of Disk Space when the VM is running. Previously when choosing Thin Provisioning for KVM to oVirt Importing, the Disk Size of the VM within the Storage Domain of oVirt was inflated to the Volume Size or Larger when the original KVM VM was much smaller.  <br><br>Result: <br><br>Now when Importing Virtual Machines from KVM to oVirt with Thin Provisioning selected, the original Disk Size of the VM is preserved.
 - [BZ 1620573](https://bugzilla.redhat.com/1620573) <b>[downstream clone - 4.2.7] [RFE] Time sync in VM after resuming from PAUSE state</b><br>Feature: <br><br>Added optional Guest Time Synchronization to the snapshot functionality via the time_sync_snapshot_enable option and other un-pausing scenarios via the time_sync_cont_enable option for synchronizing and correcting the time on the VM after long pauses. The defaults for the option are turned off for backward compatibility.<br><br>Reason: <br><br>This becomes especially critical when there are heavy loads on the VM to ensure time stamps for example are accurate.<br><br>Result: <br><br>When the options are enabled, the VDSM shall attempt to synchronize the time either during pauses that occur via during snapshots and/or during other un-pausing functionality.

#### oVirt Log Collector

 - [BZ 1620271](https://bugzilla.redhat.com/1620271) <b>enable rhv_analyzer plugin for sos >= 3.6</b><br>ovirt-log-collector now includes the RHV Log Collector Analyzer report. This analysis is generated by rhv-log-collector-analyzer tool which analyze the RHV environment and detect anomaly in the system.

### Bug Fixes

#### oVirt Engine

 - [BZ 1589045](https://bugzilla.redhat.com/1589045) <b>[RHHI] Brick profile feature in RHV-M doesn't seems to be working</b><br>

#### VDSM

 - [BZ 1627289](https://bugzilla.redhat.com/1627289) <b>[downstream clone - 4.2.7] startUnderlyingVm fails with exception resulting in split-brain</b><br>

#### oVirt Hosted Engine Setup

 - [BZ 1568841](https://bugzilla.redhat.com/1568841) <b>Cant restore hosted-engine backup at deployment</b><br>

### Other

#### VDSM JSON-RPC Java

 - [BZ 1582379](https://bugzilla.redhat.com/1582379) <b>All hosts stuck in connecting/not responding state until engine restarted</b><br>

#### oVirt image transfer daemon and proxy

 - [BZ 1621140](https://bugzilla.redhat.com/1621140) <b>add info logs to proxy (similar to daemon)</b><br>

#### oVirt Cockpit Plugin

 - [BZ 1605075](https://bugzilla.redhat.com/1605075) <b>automatic creation of storage domain misses the :/ in storage connection value</b><br>
 - [BZ 1619256](https://bugzilla.redhat.com/1619256) <b>Set performance options on gluster volume</b><br>
 - [BZ 1600883](https://bugzilla.redhat.com/1600883) <b>Remove Packages tab from gluster deployment  in cockpit ovirt</b><br>
 - [BZ 1574926](https://bugzilla.redhat.com/1574926) <b>Reusing the existing gluster configuration needs validation</b><br>
 - [BZ 1619395](https://bugzilla.redhat.com/1619395) <b>Adjusting Create Volume and Exapnd Cluster for Single Node</b><br>
 - [BZ 1590867](https://bugzilla.redhat.com/1590867) <b>Host names field should be flexible to hold longer host names in brick tab</b><br>
 - [BZ 1608660](https://bugzilla.redhat.com/1608660) <b>Support single node deployment from cockpit</b><br>
 - [BZ 1603162](https://bugzilla.redhat.com/1603162) <b>[day2] Editing the hosts in generated gdeploy config file, doesn't reflect on all the config files</b><br>

#### imgbased

 - [BZ 1614971](https://bugzilla.redhat.com/1614971) <b>Upgrading RHV-H from 4.0.X to 4.2 is failing during migrate_var</b><br>

#### oVirt Engine

 - [BZ 1620599](https://bugzilla.redhat.com/1620599) <b>[RFE] Assign more than one mdev device to a VM from RHV web UI</b><br>
 - [BZ 1613339](https://bugzilla.redhat.com/1613339) <b>Stop/Start VDO service during host Maintenance/Activate</b><br>
 - [BZ 1519777](https://bugzilla.redhat.com/1519777) <b>[downstream clone - 4.2.7] rhv manager does not show the results of the search properly</b><br>In the Administration Portal, searching for virtual machines by network label, VM emulated machine, and CPU type are not supported due to the complexity of their implementation.
 - [BZ 1626157](https://bugzilla.redhat.com/1626157) <b>NPE parsing the configuration of the HE bootstrap VM created with virt-install</b><br>
 - [BZ 1631341](https://bugzilla.redhat.com/1631341) <b>[downstream clone - 4.2.7] prepareMerge task is stuck when executing a cold merge on illegal image</b><br>
 - [BZ 1589509](https://bugzilla.redhat.com/1589509) <b>[CodeChange] Drop calls to FullList</b><br>
 - [BZ 1516445](https://bugzilla.redhat.com/1516445) <b>[RFE] Change default MAC address range (increase) and do not hard-code it</b><br>
 - [BZ 1533149](https://bugzilla.redhat.com/1533149) <b>Webadmin-Volumes - update volume snapshot cluster options when no option is selected is allowed causing an exception  - Error during ValidateFailure.: java.lang.Inde xOutOfBoundsException: Index: 0, Size: 0</b><br>
 - [BZ 1613371](https://bugzilla.redhat.com/1613371) <b>Error message when attempting to change the MAC address pool is non descriptive.</b><br>
 - [BZ 1614016](https://bugzilla.redhat.com/1614016) <b>admin portal minor css issues with badges and drawers</b><br>
 - [BZ 1593239](https://bugzilla.redhat.com/1593239) <b>Starting VM through RestAPI doesn't add cdrom with cloud-init</b><br>
 - [BZ 1526794](https://bugzilla.redhat.com/1526794) <b>[UI] - Import network > Network provider should be set by default in the drop down list</b><br>
 - [BZ 1619353](https://bugzilla.redhat.com/1619353) <b>[UI] Bond slave total values have the wrong unit</b><br>
 - [BZ 1607175](https://bugzilla.redhat.com/1607175) <b>Bond stats in gui are incorrect, showing only stats of one slave member</b><br>
 - [BZ 1511409](https://bugzilla.redhat.com/1511409) <b>[Rest] + [UI] - Report data.current.tx/rx and data.current.tx/rx.bps for bond interfaces and not only for slaves</b><br>
 - [BZ 1614345](https://bugzilla.redhat.com/1614345) <b>configure ovn-central to listening on ipv6, too.</b><br>
 - [BZ 1635229](https://bugzilla.redhat.com/1635229) <b>[downstream clone - 4.2.7] Entries for snapshot creations in the command_entities table in the database prevented access to the Admin Portal</b><br>
 - [BZ 1603150](https://bugzilla.redhat.com/1603150) <b>Potential bugs not caught because of randomized unit tests on mapping conversion between api model entities and engine business entities</b><br>
 - [BZ 1631876](https://bugzilla.redhat.com/1631876) <b>Fix dependency between engine, wildfly and wildfly overlay to make upgrades in CI easier</b><br>
 - [BZ 1632244](https://bugzilla.redhat.com/1632244) <b>[downstream clone - 4.2.7] Make sure RHV Manager will use OpenJDK 8 even when newer versions are available</b><br>
 - [BZ 1622321](https://bugzilla.redhat.com/1622321) <b>Receiving Getlldpvds error when editing host networks</b><br>
 - [BZ 1612124](https://bugzilla.redhat.com/1612124) <b>Engine raises 'insufficient permissions' error when normal user try to access /ovirt-engine/api</b><br>
 - [BZ 1619303](https://bugzilla.redhat.com/1619303) <b>Importing OVA does not honor disk size allocationUnits defined in ovf file</b><br>
 - [BZ 1609319](https://bugzilla.redhat.com/1609319) <b>failed to update cluster compatibility to version 4.2</b><br>
 - [BZ 1575586](https://bugzilla.redhat.com/1575586) <b>Active snapshot disks appears when creating VM template from snapshot instead of the snapshot disks</b><br>
 - [BZ 1623818](https://bugzilla.redhat.com/1623818) <b>[4.2.z Clone] An exception is thrown when creating a template from snapshot with less disks then the active VM</b><br>
 - [BZ 1598996](https://bugzilla.redhat.com/1598996) <b>deleteVolume task is not cleared after a failed LSM due to power off VM during snapshot creation</b><br>
 - [BZ 1613462](https://bugzilla.redhat.com/1613462) <b>When importing image from Glance, warning message is displayed</b><br>

#### VDSM

 - [BZ 1614430](https://bugzilla.redhat.com/1614430) <b>vdsm-gluster stuck on operations forcing vdsm to stop working</b><br>
 - [BZ 1613339](https://bugzilla.redhat.com/1613339) <b>Stop/Start VDO service during host Maintenance/Activate</b><br>
 - [BZ 1621211](https://bugzilla.redhat.com/1621211) <b>[downstream clone - 4.2.7] qemu-img: slow disk move/clone/import</b><br>
 - [BZ 1594194](https://bugzilla.redhat.com/1594194) <b>Make vdsm-client schema cache part of the package</b><br>
 - [BZ 1633586](https://bugzilla.redhat.com/1633586) <b>hooks/before_device_create/50_openstacknet fails</b><br>
 - [BZ 1627734](https://bugzilla.redhat.com/1627734) <b>Don't attempt unnecessary cleanups in vhostmd hook</b><br>
 - [BZ 1625098](https://bugzilla.redhat.com/1625098) <b>Wrong network threshold limit warnings on vdsm version 4.20.35-1.el7</b><br>
 - [BZ 1615414](https://bugzilla.redhat.com/1615414) <b>Unable to change CD for drivers installation while installing a system from CD</b><br>

#### oVirt Release Package

 - [BZ 1613231](https://bugzilla.redhat.com/1613231) <b>goferd errors in /var/log/messages of Red Hat Virtualization Host</b><br>

#### oVirt Hosted Engine HA

 - [BZ 1619365](https://bugzilla.redhat.com/1619365) <b>VM HostedEngine is unexpectedly down with qemu error on source host after migration is completed</b><br>
 - [BZ 1614814](https://bugzilla.redhat.com/1614814) <b>[SHE] Remove 'sudo' from _check_service on HE Hosts</b><br>

#### oVirt Hosted Engine Setup

 - [BZ 1620314](https://bugzilla.redhat.com/1620314) <b>SHE disaster recovery is broken in new 4.2 deployments as hosted_storage is master</b><br>
 - [BZ 1469908](https://bugzilla.redhat.com/1469908) <b>[RFE] - Support managed/automated restore</b><br>
 - [BZ 1622240](https://bugzilla.redhat.com/1622240) <b>"Unknown CPU model Broadwell-IBRS-SSBD"</b><br>
 - [BZ 1595384](https://bugzilla.redhat.com/1595384) <b>getent play in validate_hostname_tasks.yml results in failure when short hostname listed first in /etc/hosts</b><br>
 - [BZ 1622135](https://bugzilla.redhat.com/1622135) <b>Free space check on local bootstrap VM directory is not performed at ansible level</b><br>
 - [BZ 1624529](https://bugzilla.redhat.com/1624529) <b>hosted-engine-setup doesn't restore hostname entry of RHV manager under "/etc/hosts" at the end of the setup if the engine VM is configured with DHCP</b><br>
 - [BZ 1621015](https://bugzilla.redhat.com/1621015) <b>SHE 3.6 upgrade to 4.0 failed but engine is 4.0</b><br>

#### oVirt Ansible ManageIQ role

 - [BZ 1627020](https://bugzilla.redhat.com/1627020) <b>Role creates disks which aren't used when using ManageIQ qcow image</b><br>
 - [BZ 1627018](https://bugzilla.redhat.com/1627018) <b>Can't set region when using ManageIQ qcow image</b><br>
 - [BZ 1624836](https://bugzilla.redhat.com/1624836) <b>Specified miq_vm_disk_storage variable cause undefined disk_storage_domain variable</b><br>
 - [BZ 1613914](https://bugzilla.redhat.com/1613914) <b>engine_fqdn is undefined  in wait_for_api - while using engine_url</b><br>
 - [BZ 1614314](https://bugzilla.redhat.com/1614314) <b>ManageIQ role should support Dry Run</b><br>
 - [BZ 1592857](https://bugzilla.redhat.com/1592857) <b>ovirt-ansible-roles: Manageiq: Can't set region</b><br>
 - [BZ 1613723](https://bugzilla.redhat.com/1613723) <b>Exception during task: adding host alias of appliance cause crashing ansible</b><br>
 - [BZ 1584772](https://bugzilla.redhat.com/1584772) <b>ManageIQ role doesn't work with passed RHV Credentials from Ansible Tower</b><br>

#### oVirt Ansible image template role

 - [BZ 1576433](https://bugzilla.redhat.com/1576433) <b>Provide option to set engine FQDN as an addition to full engine URL for all roles</b><br>

#### oVirt Ansible Repositories role

 - [BZ 1548082](https://bugzilla.redhat.com/1548082) <b>[RFE] Role should find pool ids by self</b><br>

#### ovirt-engine-extension-aaa-ldap

 - [BZ 1635198](https://bugzilla.redhat.com/1635198) <b>[downstream clone - 4.2.7] ovirt-engine-extension-aaa-ldap-setup generates incorrect config for LDAP setup using multiple servers with round robin request distribution</b><br>

#### oVirt Log Collector

 - [BZ 1616370](https://bugzilla.redhat.com/1616370) <b>(EL7.6) STDERR: a non-existing plugin (general) was specified in the command line</b><br>

#### oVirt Engine WildFly

 - [BZ 1631876](https://bugzilla.redhat.com/1631876) <b>Fix dependency between engine, wildfly and wildfly overlay to make upgrades in CI easier</b><br>

#### oVirt Engine WildFly Overlay

 - [BZ 1631876](https://bugzilla.redhat.com/1631876) <b>Fix dependency between engine, wildfly and wildfly overlay to make upgrades in CI easier</b><br>

### No Doc Update

#### oVirt Engine

 - [BZ 1628883](https://bugzilla.redhat.com/1628883) <b>[BREW BUILD ENABLER] Rebase vdsm-jsonrpc-java for version 4.2.7</b><br>
 - [BZ 1618462](https://bugzilla.redhat.com/1618462) <b>UpdateVmCommand raises: "Exception: org.springframework.dao.DataIntegrityViolationException: CallableStatementCallback" after updating VM memory</b><br>

