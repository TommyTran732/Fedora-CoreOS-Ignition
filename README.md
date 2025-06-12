# Fedora-CoreOS-Ignition
Ignition configurations for Fedora CoreOS<br />

## Notes
These configurations are tailored for Metropolis.nexus environment:
- Firewalling is handled by Proxmox (not the individual VMs)
- DNSSEC validation is done by either OPNsense or a central VM dedicated to running the DNS resolver
- The `docker-auto-update@.timer` in `/etc/systemd/system` can be enabled to have automatic updates for your containers created by Docker Compose.