# RoadWarrior

This configures an enroled machine to be an enforced IPv4 internet gateway for the connecting machine using OpenVPN.

The only officially supported platform is OpenSuse 15/SLES 15.2, however the tasks should be generic enough to work on most GNU/Linux distributions.

## Usage

Add this repo as a submodule:

```
$ git submodule add https://github.com/alexblackie/rw.git roles/rw
```

Then enrol your host group:

```
- hosts: all
  roles:
  - rw
```

## Client Generation

Clients are kept in the var `openvpn_client_names`, which is a YAML list of Common Name values to generate client keys/certs for. You can override this any number of ways, but the easiest is likely to just specify it in your playbook itself:

```
- hosts: all
  vars:
    openvpn_client_names:
    - laptop02
    - desktop01
    - chad
  roles:
  - rw
```

Each entry in this list will create a folder under `/etc/openvpn/client/{{ name }}` with the client certificate, private key, CA certificate, TLS Auth key, and of course OpenVPN configuration. Simply `scp` this folder from the server and distribute it however you please.
