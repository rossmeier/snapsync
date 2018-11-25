Snap-Sync
=========

Triggers
--------
Snap-Sync is started whenever a new snapper snapshot is created or the network connection changes

Actions
-------
For each configuration:
 * check if the correct network connection is connected/the given remote is reachable
 * for each snapshot
   * check if snapshot already was backuped
     * yes => store
     * no
       * send metadata (info.xml)
       * check if backed up snapshot is available
         * yes => send diff
	 * no => send whole snapshot (should only happen on init)
       * flag snapshot as backed up
       * store

Setup
-----
 * create local config (schedule, server, etc)
 * gen ssh key
 * deploy ssh key with command restriction to server
 * setup server's `sudo`?
 * create remote config (target, quota, etc)

Usage
-----
`snapsync receive <sender> <config>`
Receive data from `<sender>` via stdin (usually via ssh) and process it according to `<config>` (for use in sudoers file)

`snapsync send <sender> <config>`
Send data after validating permissions (for use in sudoers file)

`snapsync auto`
Process all configs (usually called by daemon)

`snapsync daemon`
Start snapsync as daemon and send all newly created snapshots

`snapsync <config> [nr]`
Sync `<nr>` (or all snapshots) of `<config>`
