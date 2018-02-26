Ansible role: mpd
=========

[![MIT licensed][mit-badge]][mit-link]
[![Galaxy Role][role-badge]][galaxy-link]

Cross-platform ansible role for installation of MPD, MPC and NCMPCPP on MacOS and Linux Systems

Requirements
------------

One of the following OS (or deriviatives):
 - Debian | Ubuntu
 - MacOS (with [Homebrew][homebrew])

For MacOS:
if Homebrew is not installed on the managed host, install the following role via galaxy:

    ansible-galaxy install drew-kun.homebrew

 And include it in the playbook:

    roles:
        - drew-kun.homebrew

Role Variables
--------------

For installing only MPD set mpd_install_mpc and mpd_install_ncmpcpp to 'False'

For installing only ncmpcpp (or mpc) set the corresponding variable to 'True' and
run the playbook with role specifying tags:
    `ansible-playbook ./playbook.yml --tags 'mpc,ncmpcpp'`

OS-Agnostic:

| Variables | Description | Default|
|-----------|-------------|--------|
| **mpd_autostart** | Start mpd automatically | `yes` |
| **mpd_install_mpc** | Install mpc cli client | `yes` |
| **mpd_install_ncmpcpp** | Install ncmpcpp or not | `yes` |
| **mpd_ncmpcpp_users** | List of ncmpcpp users | `[drew, root]` |
| **mpd_ncmpcpp_mpd_host** | MPD host set in ncmpcpp configuration | `localhost` |
| **mpd_port** | Port mpd will run on | `6600` |
| **mpd_bind_to_address** | IP address on which mpd will listen | `any` |
| **mpd_name** | MPD name |`Music Player Daemon` |
| **mpd_restore_paused** | | `yes` |
| **mpd_auto_update** | | `yes` |
| **mpd_follow_inside_symlinks** | | `yes` |
| **mpd_follow_outside_symlinks** | | `no` |

OS-Specific (Mac and Linux):

| Variables | Description | Default|
|-----------|-------------|--------|
| **mpd_music_dir** | MPD music directory (set in mpd.conf) | Darwin: `/Volumes/music`; Debian: `/var/lib/mpd/music` |
| **mpd_playlist_dir** | Playlist directory (set in mpd.conf) | Darwin: `/Volumes/music/playlists`; Debian: `/var/lib/mpd/playlists` |
| **mpd_db_file** | MPD database file (set in mpd.conf) | Darwin: `~/.mpd/mpd.db`; Debian: `/var/lib/mpd/mpd.db` |
| **mpd_sticker_file** | sticker file (set in mpd.conf) | Darwin: `~/.mpd/sticker.db`; Debian: `/var/lib/mpd/sticker.db` |
| **mpd_log_file** | log file (set in mpd.conf) | Darwin: `~/.mpd/mpd.log`; Debian: `syslog` |
| **mpd_pid_file** | PID file (set in mpd.conf) | Darwin: `~/.mpd/mpd.pid`; Debian: None |
| **mpd_state_file** | state file (set in mpd.conf) | Darwin: `~/.mpd/mpdstate`; Debian: `/var/lib/mpd/mpdstate` |
| **mpd_user** | mpd user (set in mpd.conf) | Darwin: `{{ ansible_user_id }}`; Debian: `mpd` |
| **mpd_outputs** | list of output configurations for mpd.conf | Darwin: see *vars/Darwing.yml*; Debian: see *vars/Debian.yml* |

MacOS-Specific:

| Variables | Description | Default|
|-----------|-------------|--------|
| **mpd_osx_install_options** | List of homebrew installation options form MPD | see *vars/Darwing.yml* |
| **mpd_osx_ncmpcpp_install_options** | List of homebrew installation options for NCMPCPP | see *vars/Darwing.yml* |

Debian-Specific:

| Variables | Description | Default|
|-----------|-------------|--------|
| **mpd_firewall_zones** | Open MPD port only for the list of these firewalld zones | `[ public ]` |

Dependencies
------------

None

Example Playbook
----------------

    - hosts: dev_clients_macos
      roles:
        - drew-kun.homebrew
        - drew-kun.mpd

License
-------

[MIT][mit-link]

Author Information
------------------

Andrew Shagayev | [e-mail](mailto:drewshg@gmail.com)

[role-badge]: https://img.shields.io/badge/role-drew--kun.mpd-green.svg
[galaxy-link]: https://galaxy.ansible.com/drew-kun/mpd/
[mit-badge]: https://img.shields.io/badge/license-MIT-blue.svg
[mit-link]: https://raw.githubusercontent.com/drew-kun/ansible-mpd/master/LICENSE
[homebrew]: http://brew.sh/
