# BlackieOps RoadWarrior Gateway

This configures an enroled machine to be an enforced IPv4 internet gateway for
the connecting machine using OpenVPN.

Only CentOS 7.4 is supported.

## Usage

Add this repo as a submodule:

```
$ git submodule add https://bitbucket.org/blackieops/roadwarrior_gateway.git roles/roadwarrior_gateway
```

Then enrol your host group:

```
- hosts: vpnz
  roles:
    - roadwarrior_gateway
```
