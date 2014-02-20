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
to satisy the two-factor requirement.

Alternatives would be to whitelist your IP address or to only use two-factor
authentication for non-deployment accounts, but both are not handled by this role.


Requirements
------------

This role requires an active [Duo](https://www.duosecurity.com/) account.


Role Variables
--------------

This role requires three variables to be set, preferrably in the
`group_vars/all` file:

    duo:
      api_hostname: api-xxxxxxxx.duosecurity.com
      integration_key: xxx
      secret_key: xxx


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
