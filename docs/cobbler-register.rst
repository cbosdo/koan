Cobbler-Register
****************

cobbler-register - create a cobbler system record

SYNOPSIS
########

.. code-block:: shell

    cobbler-register [--server=<cobbler.example.org>] --profile=<cobbler-profile-name> [--fqdn=<hostname>]

DESCRIPTION
###########

Running cobbler-register on a system will create a cobbler system record for that system on a remote cobbler server. No
changes will be made on the system itself.

DETAILS
#######

When installing new machines into a cobbler managed datacenter/lab, it helps to not have to manually enter in the
network information for those systems. Using ``cobbler-register`` either from a kickstart or a live environment (or even
SSH) can help seed the cobbler database.

Network information is discovered automatically for all physical interfaces. ``cobbler-register`` will attempt to
discover the hostname, though if `localhost.localdomain` is found, it will have to use some other data for the cobbler
system record. This is probably not what you want, so specify ``--fqdn`` in this instance to override that registration
value.

For this to work, the ``register_new_installs`` setting must be enabled on the remote cobbler server.

When the remote system record is created, for safety reasons, it will be set in Cobbler to be "netboot disabled". Use
``cobbler system edit --name=foo --netboot-enabled=1`` to set the machine to reinstall, where "foo" is the name of the
new system record.

ENVIRONMENT VARIABLES
#####################

cobbler-register respects the `COBBLER_SERVER` variable to specify the cobbler server to use. This is a convenient way
to avoid using the ``--server`` option. This variable is set automatically on systems installed via cobbler, assuming
standard kickstart templates are used. If you need to change this on an installed system, edit
``/etc/profile.d/cobbler.{csh,sh}``.

ADDITIONAL
##########

Reading the koan manpage, www.cobbler.github.io or this Readthedocs-Project is highly recommended.

AUTHOR
######

Michael DeHaan <michael.dehaan AT gmail>

Revised by: Enno Gotthold <matrixfueller@gmail.com>
