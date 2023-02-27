# ansible-role-coredns

Install and configure CoreDNS on Linux.

## Role Variables

### General

```yaml
coredns_version: 1.10.0

coredns_install_account: coredns
coredns_install_path: /opt/coredns
coredns_dns_port: 53

coredns_service_enabled: true
coredns_service_start: true
```

### Forwarder

```yaml
# Forward DNS requests to another server
# disabling this makes this basically an only authorative server in case it serves zone files
coredns_forwarders_enabled: true
coredns_forwarders:
  # - https://cloudflare-dns.com/dns-query
  - tls://1.1.1.1
  - tls://1.0.0.1
coredns_tls_forwarder_servername: cloudflare-dns.com
```

### Plugins

```yaml
# Autoload zone files
coredns_plugin_auto_enabled: true

# Log requests
coredns_plugin_logging_enabled: false
# Log errors when processing queries
coredns_plugin_errors_enabled: true

# Minimize response data
coredns_plugin_minimal_enabled: false

# Randomize the order of A, AAAA and MX records
coredns_plugin_loadbalance_enabled: true

# Cache all responses
coredns_plugin_cache_enabled: true

# Enable prometheus metrics gathering (:9153/metrics)
coredns_plugin_prometheus_enabled: false
coredns_plugin_prometheus_listen_address: :9153
```

### Default zone

```yaml
# automatically generate a default zone
coredns_default_zone_create: true
# base domain
coredns_default_zone_domain: home.internal
coredns_default_zone_ttl: 5m
coredns_default_zone_entries: []
  # - name: postgres-1
  #   comment: Postgres Server
  #   entries:
  #     - type: A
  #       value: 192.168.1.1
  #     - type: AAAA
  #       value: fd00::abcd
  # [...]
```

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: servers
  roles:
     - { role: dschemp.coredns }
```

## License

MIT
