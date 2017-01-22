ansible-rootcrypto
==================

[![Build Status](https://travis-ci.org/systemli/ansible-rootcrypto.svg)](https://travis-ci.org/systemli/ansible-rootcrypto) [![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-rootcrypto-blue.svg)](https://galaxy.ansible.com/systemli/rootcrypto/)

Simple ansible role to maintain a existing Debian root encryption

Role Variables
--------------

The playbook requires to set your ssh keys and the crypto devices

    rootcrypto_sshkeys:
      - "ssh-rsa ..."
    rootcrypto_devices:
      -
        name: crypt-root
        device: /dev/vg0/root
        key_file: none
        options: luks
      -
        name: crypt-swap
        device: /dev/vg0/swap
        key_file: /dev/urandom
        options: swap,cipher=aes-cbc-essiv:sha256,size=256
        
Defaults:

    rootcrypto_packages:
      - cryptsetup
      - lvm2
      - busybox
      - dropbear
      - mdadm
    
    rootcrypto_network_device: eth0
    rootcrypto_network_address: "{{ ansible_default_ipv4.address }}"
    rootcrypto_network_netmask: "{{ ansible_default_ipv4.netmask }}"
    rootcrypto_network_gateway: "{{ ansible_default_ipv4.gateway }}"
    
    rootcrypt_modules:
      - r8169
      - raid0
      - raid1
      - raid456
      - md
      - aes
      - aes_i586
      - aes_x86_64
      - aes_generic
      - dm-crypt
      - dm-mod
      - sha256
      - sha256_generic
      - lrw
      - xts
      - crypto_blkcipher
      - gf128mul
    
    rootcrypto_mount_allow_shell: 0
    rootcrypto_sshkeys: []
    rootcrypto_devices: []

Download
--------

Download latest release with `ansible-galaxy`

	ansible-galaxy install systemli.rootcrypto

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: systemli.rootcrypto }

License
-------

GPLv3

Author Information
------------------

https://www.systemli.org