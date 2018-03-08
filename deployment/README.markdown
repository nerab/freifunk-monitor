# C.H.I.P. as Freifunk Monitor

This is an ansible library that deploys a fresh C.H.I.P. with all configuration and software required for running as a Freifunk Monitor.

In this document, the C.H.I.P. will be called `freifunk-monitor`, whereas the controlling machine is called `control`.

# Prepare the Control Machine

* Make sure you have a recent [Ansible installation](http://docs.ansible.com/ansible/intro_installation.html):

  ```bash
  control$ brew install ansible sshpass
  ```

  Replace `brew` with `yum` or `apt-get`, depending on your OS.

* Install the required Ansible roles:

  ```bash
  control$ ansible-galaxy install -r roles.yml
  ```

# Prepare the C.H.I.P.

* Boot the C.H.I.P. with a [fresh firmware](https://flash.getchip.com/).

* Log on at the console

  ```bash
  control$ screen /dev/tty.usbmodem*
  ```

  Use `chip` for both username and password. You may have to press ENTER to see the login screen. Exit via pressing `Control-A` and then `Control-D`.

* Connect to WiFi (Ethernet via USB works, too):

  ```bash
  sudo su -
  env TERM=linux nmtui
  ```

  Setting the TERM variable was necessary because ncurses has issues.

* Install python (required for Ansible):

  ```bash
  sudo apt-get update
  sudo apt-get -y install python
  ```

# First Deployment

The C.H.I.P. will start with the default hostname `chip` so that we need to pass that name (or its IP address) as a custom inventory:

```bash
control$ ansible-playbook -i chip, --ask-become-pass deployment/playbook.yml
```

We also need `--ask-become-password` because, other than on the Raspberry Pi, the default C.H.I.P. installation asks for the user's password when doing `sudo`. This is changed with the first deployment and `--ask-become-password` is not required afterwards.

# Subsequent Deployments

The first deployment did set the hostname to `freifunk-monitor` and also copied the public key, so that subsequent deployments become as simple as:

```bash
control$ ansible-playbook deployment/playbook.yml
```
