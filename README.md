Duo for Ansible
========

Provide two-factor authentication on your server with
[Duo](https://www.duosecurity.com/). After installation all SSH connections will
authenticate using Duo.

This means **all SSH connections**, or in other words, you can't run Ansible
sanely on the same box once this role completes and SSH is restarted. Any
SSH requests will require verifying the request via the Duo app or a passcode
and Ansible generates **A LOT** of them.

This role will setup SSH on the remote machine to allow passing a `DUO_PASSCODE`
environment variable from the control machine to allow passing in your Duo code
to satisfy the two-factor requirement.

Alternatives would be to whitelist your IP address or to only use two-factor
authentication for non-deployment accounts, but both are not handled by this role.

Note: It is possible to use SSH ControlMaster channels to enable DUO 2FA an
continue to use Ansible normally however it is blocked behind Ansible [#10065](https://github.com/ansible/ansible/issues/10065)!


Requirements
------------

This role requires an active [Duo](https://www.duosecurity.com/) account.


Role Variables
--------------

This role requires three variables to be set, preferably in the
`group_vars/all` file:

    duo:
      api_hostname: api-xxxxxxxx.duosecurity.com
      integration_key: xxx
      secret_key: xxx

To enable PAM rather than the ForcedCommand method override the role defaults.

    duo:
      use_pam: True

Note: There is a known issue with pam_duo.so path changing on different
operating systems. To workaround this update **path_to_pam_duo** to point to
 the directory containing pam_duo.so. See the DUO [Documentation](https://www.duosecurity.com/docs/duounix#pam-configuration).

    duo:
      path_to_pam_duo: /lib64/security/

Dependencies
------------

This role requires `libssl-dev` and `python-pycurl` to be installed, but they
will be added automatically by this role.


License
-------

MIT


Author Information
------------------

Created by Jonathan Knapp of [Coffee and Code](http://coffeeandcode.com).
