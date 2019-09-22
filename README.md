# Ansible Role: proxy env 
An ansible role to setup the proxy environment in shell environment ( /etc/profile & /etc/csh_cshrc ) and the package manager. The following package managers are supported: 

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
  * **env**: false (default) / text / absent. The proxy variable.
  * **no_proxy**:  false (default) / text / absent  The no_proxy variable. 
  * **protocols**: Array with the protocols to configure. Defaults ( - http, - https,  - ftp ) 
  * **etc_profile_proxy**: false / {{ proxy.env }} (default) / absent.
  * **etc_profile_no_proxy**: false / {{ proxy.no_proxy }} (default) / absent.
  * **etc_csh_cshrc_proxy**: false / {{ proxy.env }} (default) / absent.
  * **etc_csh_cshrc_no_proxy**: false / {{ proxy.no_proxy }} (default) / absent.
  * **pkg_mgr_proxy**: false / {{ proxy.env }} (default) / absent.

Proxy setting variables;

  * **false or undef:**
    The no_proxy/proxy environment are not altered.
  * **text:**
    The no_proxy/proxy environment are updated to text. 
  * **absent:**
    The no_proxy/proxy environment is removed

## Dependencies

None

## Example Playbooks

### Configure the proxy environment
 
```
- name: setup proxy on internal hosts
  hosts: all:!dmz:!k8s
  become: true
  vars:
    proxy:
      env: "http://proxy:3128"
  roles:
    - stafwag.proxy_env
```

### Configure the proxy in the pkg_mgr, and remove it from the shell environment.  

```
- name: setup proxy on k8s hosts
  hosts: k8s
  become: true
  vars:
    proxy:
      env: absent
      no_proxy: absent
      pkg_mgr_proxy: http://proxy:3128
  roles:
    - stafwag.proxy_env
```

### Remove the proxy settings

```
- name: setup proxy
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
