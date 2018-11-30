# nginx

[![Build Status](https://travis-ci.com/iroquoisorg/ansible-role-nginx.svg?branch=master)](https://travis-ci.com/iroquoisorg/ansible-role-memcached)

Ansible role for nginx

This role was prepared and tested for Ubuntu 16.04.

# Installation

`$ ansible-galaxy install iroquoisorg.nginx`

# Default settings

```

nginx_redhat_pkg:
  - nginx

nginx_ubuntu_pkg:
  - python-selinux
  - nginx

nginx_freebsd_pkg:
  - nginx

nginx_suse_pkg:
  - nginx

nginx_install_epel_repo: true

nginx_official_repo: false
nginx_official_repo_mainline: false
nginx_ubuntu_ppa: false

keep_only_specified: false

nginx_installation_type: "packages"
nginx_binary_name: "nginx"
nginx_service_name: "{{nginx_binary_name}}"
nginx_conf_dir: "{% if ansible_os_family == 'FreeBSD' %}/usr/local/etc/nginx{% else %}/etc/nginx{% endif %}"

nginx_user: "{% if ansible_os_family == 'RedHat' or ansible_os_family == 'Suse' %}nginx{% elif ansible_os_family == 'Debian' %}www-data{% elif ansible_os_family == 'FreeBSD' %}www{% endif %}"
nginx_group: "{{nginx_user}}"

nginx_pid_file: '/var/run/{{nginx_service_name}}.pid'

nginx_worker_processes: "{% if ansible_processor_vcpus is defined %}{{ ansible_processor_vcpus }}{% else %}auto{% endif %}"
nginx_worker_rlimit_nofile: 1024
nginx_log_dir: "/var/log/nginx"
nginx_error_log_level: "error"

nginx_events_params:
  - worker_connections {% if nginx_max_clients is defined %}{{nginx_max_clients}}{% else %}512{% endif %}

nginx_http_params:
  - sendfile "on"
  - tcp_nopush "on"
  - tcp_nodelay "on"
  - keepalive_timeout "65"
  - access_log "{{nginx_log_dir}}/access.log"
  - "error_log {{nginx_log_dir}}/error.log {{nginx_error_log_level}}"
  - server_tokens off
  - types_hash_max_size 2048

nginx_stream_params: []

nginx_sites: {}
nginx_remove_sites: []

nginx_configs: {}
nginx_stream_configs: {}
nginx_remove_configs: []

nginx_auth_basic_files: {}
nginx_remove_auth_basic_files: []

nginx_daemon_mode: "on"

nginx_server_names_hash_bucket_size: 64

```

# Development

Please check [development guide](DEVELOPMENT.md) for details about developing and testing this role.
