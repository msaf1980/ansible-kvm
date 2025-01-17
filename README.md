# ansible-kvm

An [Ansible](https://www.ansible.com) role to install [KVM](https://www.linux-kvm.org/page/Main_Page)

## Build Status

[![Build Status](https://travis-ci.org/mrlesmithjr/ansible-kvm.svg?branch=master)](https://travis-ci.org/mrlesmithjr/ansible-kvm)

## Requirements

Install [required](./requirements.yml) [Ansible](https://www.ansible.com) roles:

```bash
sudo ansible-galaxy install -r requirements.yml
```

## Role Variables

[defaults/main.yml](defaults/main.yml)

## Dependencies

None

## Example Playbook

```yaml
- hosts: kvm_hosts
  vars: {}
  roles:
    - role: ansible-kvm
  tasks: []
```

## Booting a VM from ISO

You can boot a defined VM up with an ISO by using the following example:

> NOTE: Defined in your vars. Also, ensure that the default
> `kvm_manage_vms: false` is changed to `kvm_manage_vms: true`.

```yaml
kvm_manage_vms: true
kvm_vms:
  - name: test_vm
    autostart: true
    # Define boot devices in order of preference
    boot_devices:
      - cdrom
      - network
      - hd
    cdrom:
      source: /path/to/iso
    graphics: false
    # Define disks in MB
    disks:
      - disk_driver: virtio
        name: test_vm.1
        size: 36864
    memory: 512
    network_interfaces:
      - source: default
        network_driver: virtio
        portgroup: vlan-102
        type: network
    state: running
    vcpu: 1
```


## Example Vars for configure networks

kvm_config_virtual_networks: true
kvm_virtual_networks:
  - name: 'default'
    bridge_name: 'virbr0'
    mode: 'nat'
    state: 'active'
    autostart: 'true'
    enable_dhcp: true
    ip: '192.168.122.1'
    netmask: '255.255.255.0'
    dhcp_scope_start: '192.168.122.2'
    dhcp_scope_end: '192.168.122.254'
  - name: 'lan'
    bridge_name: 'virbr1'
    mode: 'routed'
    state: 'active'
    autostart: 'true'
    ip: '192.168.0.2'
    netmask: '255.255.255.0'


## License

MIT

## Author Information

Larry Smith Jr.

- [@mrlesmithjr](https://www.twitter.com/mrlesmithjr)
- [EverythingShouldBeVirtual](http://everythingshouldbevirtual.com)
- [mrlesmithjr@gmail.com](mailto:mrlesmithjr@gmail.com)
