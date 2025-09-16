`repositories`
=========

This role configures the enabled repositories on your Proxmox nodes.

Requirements
------------

No requirements. 

Role Variables
--------------

`enterprise`: This variable can be configured at the host_vars or group_vars level to indicate whether a node or group of nodes has enterprise licensing. If set to `true`, the role will configure enterprise sources. Default is `false`.

Dependencies
------------

No dependencies.

Example Playbook
----------------

    - hosts: servers
      roles:
         - repositories
License
-------

MIT

Author Information
------------------

Taylor Cohron  

* [Email](taylorcohrontech@gmail.com)
* [GitHub](https://github.com/untraceablez)
* [Website](https://taylorcohron.me)