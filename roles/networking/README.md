`networking`
=========

This role configures all of your physical and virtual bridge interfaces on your Proxmox nodes.

Requirements
------------

`vmbr0` should already be configured on each node prior to running this configuration. 

Role Variables
--------------

`net_type`: This variable determines which template is used for `etc/network/interfaces`.
  * If `linux-bonds` is defined, the configuration is setup to use Linux bonds to create the virtual bridges.
  * If `ovs-bonds` is defined, the configuration is setup to use OVS bonds to create the virtual bridges.
  * If `linux-bridges` is defined, the configuration is setup to map physical interfaces directly to bridges.
  * If `ovs-bridges` is defined, the configuration is setup to map physical interfaces directly to bridges.

Dependencies
------------

No dependencies.

Example Playbook
----------------

    - hosts: servers
      roles:
         - networking

License
-------

MIT

Author Information
------------------

Taylor Cohron  

* [Email](taylorcohrontech@gmail.com)
* [GitHub](https://github.com/untraceablez)
* [Website](https://taylorcohron.me)