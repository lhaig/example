# Example Nomad Levant Deployment
This is an example levant Deployment that can be used as a base for creating other deployments.

This is the standard `nomad init` specification that has been converted to a Levant style deployment.

## Prerequisites

* Deploy a Nomad Cluster or Developer instance <https://www.nomadproject.io/docs/install>
* Consul should also be installed as Fabio uses this for discovery
* Download [Levant]<https://github.com/hashicorp/levant>

## Usage

Download the repository and then alter the example.nomad file and the variables.yaml file to match your deployment requirements.

Then follow Levant deployment workflow to deploy the example.