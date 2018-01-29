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

    mpd_autostart: yes | no                 # start mpd automatically
    mpd_install_mpc: yes | no
    mpd_install_ncmpcpp: yes | no           # Install ncmpcpp or not
    mpd_ncmpcpp_users:                      # list of ncmpcpp users
    mpd_port:                               # port mpd will run on
    mpd_bind_to_address:                    # IP address on which mpd will listen
    mpd_name:                               # MPD name
    mpd_restore_paused: yes | no            #
    mpd_auto_update: yes | no               #
    mpd_follow_inside_symlinks: yes | no    #
    mpd_follow_outside_symlinks: yes | no   #

OS-Specific (Mac and Linux):

    # Configuration related vars:
    mpd_music_dir:                          # MPD music directory (set in mpd.conf)
    mpd_playlist_dir:                       # Playlist directory (set in mpd.conf)
    mpd_db_file:                            # MPD database file (set in mpd.conf)
    mpd_sticker_file:                       # sticker file (set in mpd.conf)
    mpd_log_file:                           # log file (set in mpd.conf)
    mpd_pid_file:                           # PID file (set in mpd.conf)
    mpd_state_file:                         # state file (set in mpd.conf)
    mpd_user:                               # mpd user (set in mpd.conf)
    mpd_outputs:                            # list of output configurations for mpd.conf

MacOS-Specific:

    mpd_osx_install_options:                # Homebrew install options form MPD
    mpd_osx_ncmpcpp_install_options:        # Homebrew install options for NCMPCPP

Debian-Specific:

    mpd_firewall_zones:                     # Open MPD port only for these firewalld zones (list)

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

Andrew Shagayev

[role-badge]: https://img.shields.io/badge/role-drew--kun.mpd-green.svg
[galaxy-link]: https://galaxy.ansible.com/drew-kun/mpd/
[mit-badge]: https://img.shields.io/badge/license-MIT-blue.svg
[mit-link]: https://raw.githubusercontent.com/drew-kun/ansible-mpd/master/LICENSE
[homebrew]: http://brew.sh/
