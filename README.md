# Ansible Role: proxy env 
An ansible role to setup the proxy settings in shell environment ( /etc/profile & /etc/csh_cshrc )
and the package manager. The following package managers are supported: 

* apt
* pacman
* pkgng
* Suse (on Suse /etc/sysconfig/proxy is configured)
* yum
 
## Requirements

None

## Role Variables

### Playbook related variables

* **proxy**:
  * **env**: the proxy setting.
  * **protocols**: Array with the protocols to configure. Defaults ( - http, - https,  - ftp ) 
  * **etc_profile_config**: false / true (default) 
  * **etc_csh_cshrc_config**: false / true (default)
  * **pkg_mgr_config**: false / true (default) 

## Dependencies

None

## Example Playbooks

### Configure the proxy in the pkg_mgr  

```
- name: setup proxy
  hosts: all
  become: true
  vars:
    proxy:
      env: "http://proxyhost:3128"
      etc_csh_cshrc_config: no
      etc_profile_config: no
  roles:
    - stafwag.proxy_env
```

### Remove the proxy settings

```
- name: remove proxy from shell environment
  hosts: all
  become: true
  vars:
    proxy:
      env: absent
  roles:
    - stafwag.proxy_env
```

## License

MIT/BSD

## Author Information

Created by Staf Wagemakers, email: staf@wagemakers.be, website: http://www.wagemakers.be.
