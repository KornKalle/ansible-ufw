# UFW Role

This Ansible role manages UFW (Uncomplicated Firewall) settings on Debian-based systems.

## Requirements

- Ansible 2.1 or higher
- Debian-based system

## Role Variables

The following variables can be set to customize the role's behavior:

| Variable                      | Description                                                                 | Default Value |
|-------------------------------|-----------------------------------------------------------------------------|---------------|
| `ufw_default_incoming_policy` | Default policy for incoming traffic (e.g., `deny` or `allow`).              | `deny`        |
| `ufw_default_outgoing_policy` | Default policy for outgoing traffic (e.g., `allow` or `deny`).              | `allow`       |
| `ufw_rules`                   | List of UFW rules to apply. Each rule can have the following attributes:    |               |
| `rule`                        | The rule action (e.g., `allow`, `deny`, `reject`, `limit`).                 |               |
| `port`                        | The port number or range.                                                   |               |
| `proto`                       | The protocol (default is `tcp`).                                            | `tcp`         |
| `direction`                   | The direction of the traffic (`in` or `out`, default is `in`).              | `in`          |
| `from_ip`                     | The source IP address (default is `any`).                                   | `any`         |
| `to_ip`                       | The destination IP address (default is `any`).                              | `any`         |
| `delete`                      | Whether to delete the rule (default is `false`).                            | `false`       |
| `log`                         | Whether to log the rule (default is `false`).                               | `false`       |
| `name`                        | A comment for the rule.                                                     |               |
| `ufw_enabled`                 | Whether to enable UFW (default is `true`).                                  | `true`        |

## Dependencies

None.

## Example Playbook

```yaml
- hosts: servers
  roles:
    - role: ufw
      ufw_default_incoming_policy: deny
      ufw_default_outgoing_policy: allow
      ufw_rules:
        - { rule: allow, port: 22, proto: tcp, direction: in, from_ip: any, to_ip: any, log: true, name: 'Allow SSH' }
        - { rule: allow, port: 80, proto: tcp, direction: in, from_ip: any, to_ip: any, log: false, name: 'Allow HTTP' }
      ufw_enabled: true