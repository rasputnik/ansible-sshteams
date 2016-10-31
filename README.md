SSH team management
===================

**very much work in progress - choking hazard, traces of nuts etc.**

Manage team access to servers

  * create user accounts
  * setup user SSH pubkey access
  * toggle passwordless sudo access to teams

implementation
==============

There are 2 dinky centos vms just to have something to work with.

    vagrant up
    ansible-playbook -i inv/ ssh.yml 

vars
====

There are 2 main sets of config

The first set is 'static' - a definitive access list

  * dict of teams listing user accounts
  * a pubkey file for each user

The other config is per-host/inventory/group vars

  * a list of which teams can SSH in
  * a list of which teams can sudo

management
==========

Here are the sort of operations we should support. I haven't
figured them all out yet.

  * user joins team: update group dict, add pubkey
  * user key compromise: update pubkey, run play
  * user goes rogue/leaves: truncate pubkey, run play
  * grant team sudo access: set var on inventory/group/host
  * revoke team sudo access: update var on inventory/group/host
  * user leaves team: ??? - maybe one-off playbook?
  * single user 'team': so be it (code smell, but supported).
  * multiple teams for user: unsupported. team == unix group.

bugs
====

I would lay money on it. If anyone has a cleaner way to do this,
_please_ file a PR/issue.
