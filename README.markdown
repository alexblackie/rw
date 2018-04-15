# BlackieOps RoadWarrior Gateway

This configures an enroled machine to be an enforced IPv4 internet gateway for
the connecting machine using OpenVPN.

Only CentOS 7 is supported.

## Usage

Add this repo as a submodule:

```
$ git submodule add https://projects.blackieops.com/blackieops/roadwarrior_gateway.git roles/roadwarrior_gateway
```

Then enrol your host group:

```
- hosts: rws
  roles:
    - roadwarrior_gateway
```

## Client Generation

Clients are kept in the var `openvpn_client_names`, which is a YAML list of
Common Name values to generate client keys/certs for. You can override this any
number of ways, but the easiest is likely to just specify it in your playbook
itself:

```
- hosts: rws
  vars:
    openvpn_client_names:
      - laptop02
      - edgep2p
      - desktop01
  roles:
    - roadwarrior_gateway
```

Each entry in this list will create a folder under
`/etc/openvpn/client/{{ name }}` with the client certificate, private key, CA
certificate, TLS Auth key, and of course OpenVPN configuration. Simply `scp`
this folder from the server and distribute it however you please.
