# ansible-role-sshd

Configure sshd.

# Requirements

None

# Role Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `sshd_user` | User name of `sshd` | `sshd` |
| `sshd_group` | Group name of `sshd` | `{{ __sshd_group }}` |
| `sshd_service` | Service name of `sshd` | `{{ __sshd_service }}` |
| `sshd_conf_dir` | Path to directory where `sshd` configuration files are kept | `{{ __sshd_conf_dir }}` |
| `sshd_conf` | Path to `sshd_config` | `{{ sshd_conf_dir }}/sshd_config` |
| `sshd_sftp_server` | Path to `stfp-server(8)` | `{{ __sshd_sftp_server }}` |
| `sshd_config` | Content of `sshd_config` | `""` |

## Debian

| Variable | Default |
|----------|---------|
| `__sshd_group` | `ssh` |
| `__sshd_conf_dir` | `/etc/ssh` |
| `__sshd_sftp_server` | `/usr/lib/sftp-server` |
| `__sshd_service` | `ssh` |

## FreeBSD

| Variable | Default |
|----------|---------|
| `__sshd_group` | `sshd` |
| `__sshd_conf_dir` | `/etc/ssh` |
| `__sshd_sftp_server` | `/usr/libexec/sftp-server` |
| `__sshd_service` | `sshd` |

## OpenBSD

| Variable | Default |
|----------|---------|
| `__sshd_group` | `sshd` |
| `__sshd_conf_dir` | `/etc/ssh` |
| `__sshd_sftp_server` | `/usr/libexec/sftp-server` |
| `__sshd_service` | `sshd` |

## RedHat

| Variable | Default |
|----------|---------|
| `__sshd_group` | `ssh` |
| `__sshd_conf_dir` | `/etc/ssh` |
| `__sshd_sftp_server` | `/usr/lib/sftp-server` |
| `__sshd_service` | `sshd.service` |

# Dependencies

None

# Example Playbook

```yaml
- hosts: localhost
  roles:
    - ansible-role-sshd
  vars:
    sshd_config: |
      Port 2022

      PasswordAuthentication no
      PermitRootLogin without-password
      Port 22
      UseDNS no
      {% if ansible_os_family != 'OpenBSD' %}
      UsePAM no
      {% endif %}
      Subsystem sftp {{ sshd_sftp_server }}
      Match Address 192.168.1.1
        PasswordAuthentication yes
      Match User foo
        X11Forwarding yes
      Match User bar
        X11Forwarding no
```

# License

```
Copyright (c) 2016 Tomoyuki Sakurai <tomoyukis@reallyenglish.com>

Permission to use, copy, modify, and distribute this software for any
purpose with or without fee is hereby granted, provided that the above
copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
```

# Author Information

Tomoyuki Sakurai <y@trombik.org>

This README was created by [ansible-role-init](https://gist.github.com/trombik/d01e280f02c78618429e334d8e4995c0)
