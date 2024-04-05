# Ansible Role: Commando VM ([Ludus](https://ludus.cloud))

An Ansible Role that sets up [Commando VM](https://github.com/mandiant/commando-vm) on Windows >= 10 hosts.

Uses code from [privacy.sexy](https://privacy.sexy) to disable Defender and Tamper Protection.

## Requirements

- Windows >= 10
- at least 60 GB of disk space (80+ recommended)
- at least 2GB RAM (4+ recommended)

## Role Variables

    # Disable the red/green dynamic Ludus wallpaper in favor of the static Commando VM wallpaper
    ludus_commandovm_use_commandovm_wallpaper: true
    # Use the -noPassword option if the user is set for auto-login (default: true)
    ludus_commandovm_nopassword: true
    # Provide the user's password if the user is not set for auto-login
    ludus_commandovm_password:

## Dependencies

- community.windows

## Troubleshooting

See [Troubleshooting](https://github.com/mandiant/commando-vm/blob/main/Docs/Troubleshooting.md)

## Known issues

After the first reboot the commando process may reboot again before ansible can remove the Run key that starts the install and it will fail in the background. This has no impact on the install.

## Example Playbook

```yaml
- hosts: commandovm_hosts
  roles:
    - badsectorlabs.ludus_commandovm
```

## Example Ludus Range Config

```yaml
ludus:
  - vm_name: "{{ range_id }}-commando"
    hostname: "{{ range_id }}-COMMANDO"
    template: win11-22h2-x64-enterprise-template
    vlan: 99
    ip_last_octet: 4
    ram_gb: 8
    cpus: 4
    windows:
      install_additional_tools: false
    roles:
      - badsectorlabs.ludus_commandovm
```

## License

GPLv3

## Author Information

This role was created by [Bad Sector Labs](https://github.com/badsectorlabs), for [Ludus](https://ludus.cloud/).
