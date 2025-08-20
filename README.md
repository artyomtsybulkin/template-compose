# template-compose

My compose file template and guideline

Healthcheck examples:

```yaml
test: ["CMD-SHELL", "pidof <process_name> || exit 1"]
test: ["CMD-SHELL", "curl -f http://localhost:3000/api/health"]
```

User definition examples:

```yaml
user: "472:0"
user: "10001:10001"
```

Network configuration examples:

```bash
podman network create --driver bridge \
--subnet 10.10.90.0/24 --gateway 10.10.90.1 public_net
podman network create --driver bridge \
--subnet 10.10.91.0/24 --gateway 10.10.91.1 --internal private_net
```

```yaml
# Expose port 3000 to private network only
networks: [ private_net ]
expose: [ "3000" ]

# Expose port to public only
networks: [ public_net ]
ports: ["0.0.0.0:3000:3000/udp", "0.0.0.0:3000:3000/tcp"]

# Example for ingress
networks: [ private_net, public_net ]
ports: ["0.0.0.0:3000:3000/udp", "0.0.0.0:3000:3000/tcp"]
```
