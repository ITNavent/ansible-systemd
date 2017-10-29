# Ansible Role: systemd

An Ansible role that manages systemd unit and override files on Debian/Ubuntu.

systemd Overview
--------------

Systemd manages services using unit files stored in `/usr/lib64/systemd/system`. Two methods of customizing
their behavior are [1.] copying them to `/etc/systemd/system` and modifying the local verison or [2.] adding
an override values to `/etc/systemd/system/your-service-name.d/override.conf`.

This role allows you to manage both methods.

Example Configuration
--------------

systemd_services:
  docker_container:
    - systemd_Service_ExecStart: 'dockerd'
    - systemd_Service_Type: 'simple'
    - systemd_Service_Restart: 'on-failure'
    - systemd_Install_WantedBy: 'multi-user.target'


Role Variables
--------------

|name                |type    |default|description
|--------------------|--------|-------|-------------
|`systemd_default_dir`|String|"/etc/default"|envs file path
|`systemd_unit_dir`|String|"/etc/systemd/system"|systemd path
|`systemd_environment_vars`|MapList|[]|envs (/etc/default/:name)
|`systemd_services` * |MapList|[]|service name
|`systemd_overrides` * |MapList|[]|service name

Service Variables
-----------------


|name                |type    |default|description
|--------------------|--------|-------|-------------
|`Service_Name` *|String||name of the service (../service/`Service_Name.service`)


### [Unit]


|name                |type    |default|description
|--------------------|--------|-------|-------------
|`Unit_Description`|String||[Unit]Description
|`Unit_Documentation`|String||[Unit]Documentation
|`Unit_Requires`|String,List||[Unit]Requires
|`Unit_Wants`|String,List||[Unit]Wants
|`Unit_ConditionPathExists`|String||[Unit]ConditionPathExists
|`Unit_After`|String,List||[Unit]After
|`Unit_Before`|String,List||[Unit]Before


### [Service]


|name                |type    |default|description
|--------------------|--------|-------|-------------
|`Service_Type`|String|"simple"|[Service]Type
|`Service_ExecStartPre`|String,List||[Service]ExecStartPre
|`Service_ExecStart` * |String||[Service]ExecStart
|`Service_ExecStartPost`|String,List||[Service]ExecStartPost
|`Service_Restart`|String|"no"| [Service]Restart "no" or "always" or "on-success" or "on-failure"
|`Service_RestartSec`|Integer|| [Service]RestartSec
|`Service_ExecReload`|String|| [Service]ExecReload
|`Service_ExecStop`|String|| [Service]ExecStop
|`Service_KillMode`|String|| [Service]KillMode
|`Service_ExecStopPost`|String,List|| [Service]ExecStopPost
|`Service_PIDFile`|String|| [Service]PIDFile
|`Service_BusName`|String|| [Service]BusName
|`Service_PrivateTmp`|String|| [Service]PrivateTmp
|`Service_LimitNOFILE`|String|| [Service]LimitNOFILE
|`Service_User`|String|| [Service]User
|`Service_Group`|String|| [Service]Group
|`Service_WorkingDirectory`|String|| [Service]WorkingDirectory



### [Install]

|name                |type    |default|description
|--------------------|--------|-------|-------------
|`Install_WantedBy`|String|"multi-user.target"|[Install]WantedBy
|`Install_RequiredBy`|String||[Install]RequiredBy
|`Install_Also`|String||[Install]Also
|`Install_Alias`|String||[Install]Alias


> * Required

Dependencies / Requirements
---------------------------

- None

Credits
-------

- Template files borrowed from [tumf/ansible-role-systemd-service](https://github.com/tumf/ansible-role-systemd-service)

Author and License
------------------

Chad Sheets - [GitHub](https://github.com/cjsheets) | [Blog](http://chadsheets.com/) | [Email](mailto:chad@linconf.com)

Released under the [MIT License](https://tldrlegal.com/license/mit-license)

[![Analytics](https://cjs-beacon.appspot.com/UA-10006093-3/github/linconf/ansible-role-systemd?pixel)](https://github.com/linconf/ansible-role-systemd)