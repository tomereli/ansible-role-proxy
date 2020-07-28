# Ansible Role: Proxy

[![Build Status](https://travis-ci.org/tomereli/ansible-role-proxy.svg?branch=master)](https://travis-ci.org/tomereli/ansible-role-proxy)

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):
    
    http_proxy: "{{ ansible_env.http_proxy }}"
    https_proxy: "{{ ansible_env.https_proxy }}"
    ftp_proxy: "{{ ansible_env.ftp_proxy }}"
    no_proxy: "{{ ansible_env.no_proxy }}"

The proxy variables are taken by default from the host machine via `ansible_env`. Override them if the proxy configured differs from the host. These are used to set up `/etc/environment` and the package manager (apt/yum) proxies.

    install_docker_service_proxy: true
    install_docker_containers_proxy: true
    username: "{{ ansible_user | default('root') }}"

The `install_docker_service_proxy` variable controls whether or not to install docker service proxy (`/etc/systemd/system/docker.service.d/proxy.conf`), which allows the docker service to access the internet when running behind proxy server - meaning that docker can fetch images from the internet.

The `install_docker_containers_proxy` variable controls whether or not to install docker container proxy (`~/.docker/config.json`) in the specified `username` home directory. It is assumed that the home directory is at `/home/{{ username }}`. This allows docker containers to access the internet behind proxy.

## Dependencies

None.

## Example Playbook

```yaml
- hosts: all
  roles:
    - tomereli.proxy
```

## License

MIT / BSD

## Author Information

This role was created in 2020 by [Tomer Arbel-Eliyahu](https://github.com/tomereli)
