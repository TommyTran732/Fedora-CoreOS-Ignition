# Fedora-CoreOS-Ignition
Ignition configurations for Fedora CoreOS<br />

# Notes
1. These are the configs I personally use on my systems. You **MUST** edit the files before you use them. At the very least, you should add your SSH keys or password hash.<br />
2. Only ED25519 SSH keys are accepted with the SSHD hardening configuration. If you do not use ED25519 keys, you will need to adjust the `/etc/ssh/sshd_config.d/10-custom.conf` file accordingly.
3. If you create a passwordless user that requires administrative privileges, ensure that it is part of the `sudo` group (CoreOS allows this group to use sudo without a password) as the configs will disable empty password system authentication.
4. These configurations are made with a VPS in mind. You should adapt it for a bare metal deployment if that is what you are using (adding additional kernel parameters, configuring drive encryption, configuring storage, etc). You should also change the tuned profile from `virtual-guest` appropriately.
5. The docker-compose-updater.service in `/etc/systemd/system` can be enabled to have automatic updates for your containers created by Docker Compose. Please make sure that the `WorkingDirectory` is appropriate.

# Upgrading from Fedora CoreOS 40 to 41

I am aware of a dependency issue which may cause the system to not automatically update itself to FCOS 41. To fix the problem, run:

```
systemctl stop zincati
rpm-ostree remove docker-ce
rpm-ostree override reset --all
rpm-ostree upgrade
rpm-ostree override remove cifs-utils containerd docker-cli dnsmasq google-compute-engine-guest-configs-udev iptables-legacy iptables-legacy-libs moby-engine runc samba-client-libs samba-common libwbclient libsmbclient samba-common-libs sssd-client sssd-ldap sssd-common sssd-krb5-common sssd-nfs-idmap sssd-ad sssd-krb5 sssd-ipa sssd-common-pac systemd-resolved
rpm-ostree install docker-ce
reboot
```
