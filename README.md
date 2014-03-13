pam_ssh_agent_auth
==================

PAM module to authenticate sudo though ssh-agent.

This is meerly a package for 64-bit RHEL/CentOS 6 (el6) so I can better distribute the module through Salt without having to hack together a script that wgets and builds from source every time.

Built and tested on RHEL 6.5, should be compatible with all RHEL 6 and equivalent.

This is current (0.9.5) as of this writing (Feb 2014).

The module was last updated April 2013.

Project page: http://pamsshagentauth.sourceforge.net/

Installation
------------

Install the rpm as usual, ```yum install <name>.rpm```

Add the following line in /etc/pam.d/sudo directly before the ```auth include``` line

```
auth       sufficient        pam_ssh_agent_auth.so file=~/.ssh/authorized_keys
```

Add the following line to /etc/sudoers (use visudo) after the rest of the ```Defaults env_keep``` lines.

```
Defaults    env_keep += "SSH_AUTH_SOCK"
```

Troubleshooting
---------------

* Make sure the module is installed

```
rpm -qa | grep pam_ssh
```

* Ensure your account has sudo access
* Connect using the -A flag on ssh, this enables key passthrough
* Check /var/log/secure for any errors. They might look like this, showing the module isn't in the place PAM expected

```
sudo: PAM unable to dlopen(/lib64/security/pam_ssh_agent_auth.so): /lib64/security/pam_ssh_agent_auth.so: cannot open shared object file: No such file or directory
sudo: PAM adding faulty module: /lib64/security/pam_ssh_agent_auth.so
```
