`ssh`
=========

This role configures SSH on your Proxmox nodes.

Requirements
------------

You will need Ansible Vault setup already. 

You will need your SSH keys pregenerated and encrypted by Ansible Vault. Place the **encrypted** files in `roles/ssh/files`. You will also need to encrypt the passphrase as a variable in your group_vars or host_vars. You can do so using the commands below: 

```bash
ansible-vault encrypt_string --name 'ssh_keyname' 'my-ssh-keyname'
```
You should get a result something like this:

```yaml
ssh_keyname: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          31613739643338363131653237346634346434643934653836323736373062386630396562646237
          6633313566643065343238323930663438373335666131610a386630666561613432613239346235
          66373938646334623063373633623136373661383137643466323832656535306331346439646666
          3561303632336630360a333435626639326465373136306363613730636365643136313837623034
          6632
```

Role Variables
--------------

The aforementioned `ssh_keyname` to describe the name of your ssh key. 

Dependencies
------------

No dependencies.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - ssh


License
-------

MIT

Author Information
------------------

Taylor Cohron  

* [Email](taylorcohrontech@gmail.com)
* [GitHub](https://github.com/untraceablez)
* [Website](https://taylorcohron.me)