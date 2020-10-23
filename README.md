# Example Nomad Levant Deployment
This is an example levant Deployment that can be used as a base for creating other deployments.

This is the standard `nomad init` specification that has been converted to a Levant style deployment.

## Project Website
<https://nomadproject.io>

## Prerequisites

* Deploy a Nomad Cluster or Developer instance <https://www.nomadproject.io/docs/install>
* Consul should also be installed as Fabio uses this for discovery
* Download [Levant]<https://github.com/hashicorp/levant>

## Usage

Download the repository and then alter the example.nomad file and the variables.yaml file to match your deployment requirements.

## Deploy

To deploy the example to your nomad cluster using levant use this command:

```bash
levant deploy -log-level=debug -var-file=variables.yaml  example.nomad
```

## Variables
```yaml
# Deployment Destination
datacenter: "dc1"
region: "global"

# Update
update:
  max_parallel: "1"
  min_healthy_time: "10s"
  healthy_deadline: "3m"
  progress_deadline: "10m"
  auto_revert: false
  canary: 0

# Migrate
migrate:
  max_parallel: 1
  health_check: "checks"
  min_healthy_time: "10s"
  healthy_deadline: "5m"

# Group
group:
  count: 1
  restart:
    attempts: 2
    interval: "30m"
    delay: "15s"
    mode: "fail"
  ephemeral_disk:
    sticky: true
    migrate: true
    size: 300
  task:
    driver: "docker"
    config:
      image: "redis:3.2"
      port_map:
        db: 6379
    logs:
      max_files: 10
      max_file_size: 15
    resources:
      cpu: 500
      memory: 512
      network:
        mbits: 1
    service:
      name: "redis-cache"
      tags: ['"global", "cache"']
 
 ```
