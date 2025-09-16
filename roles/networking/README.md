`networking`
=========

This role configures all of your physical and virtual bridge interfaces on your Proxmox nodes.

Requirements
------------

`vmbr0` should already be configured on each node prior to running this configuration. 

Role Variables
--------------


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