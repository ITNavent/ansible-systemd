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


### [Unit]


|name                |type    |default|description
|--------------------|--------|-------|-------------
|`systemd_Unit_Description`|String||[Unit]Description
|`systemd_Unit_Documentation`|String||[Unit]Documentation
|`systemd_Unit_Requires`|String,List||[Unit]Requires
|`systemd_Unit_Wants`|String,List||[Unit]Wants
|`systemd_Unit_ConditionPathExists`|String||[Unit]ConditionPathExists
|`systemd_Unit_After`|String,List||[Unit]After
|`systemd_Unit_Before`|String,List||[Unit]Before


### [Service]


|name                |type    |default|description
|--------------------|--------|-------|-------------
|`systemd_Service_Type`|String|"simple"|[Service]Type
|`systemd_Service_ExecStartPre`|String,List||[Service]ExecStartPre
|`systemd_Service_ExecStart` * |String||[Service]ExecStart
|`systemd_Service_ExecStartPost`|String,List||[Service]ExecStartPost
|`systemd_Service_Restart`|String|"on-failure"| [Service]Restart "no" or "always" or "on-success" or "on-failure"
|`systemd_Service_RestartSec`|Integer|| [Service]RestartSec
|`systemd_Service_ExecReload`|String|| [Service]ExecReload
|`systemd_Service_ExecStop`|String|| [Service]ExecStop
|`systemd_Service_KillMode`|String|| [Service]KillMode
|`systemd_Service_ExecStopPost`|String,List|| [Service]ExecStopPost
|`systemd_Service_PIDFile`|String|| [Service]PIDFile
|`systemd_Service_BusName`|String|| [Service]BusName
|`systemd_Service_PrivateTmp`|String|| [Service]PrivateTmp
|`systemd_Service_LimitNOFILE`|String|| [Service]LimitNOFILE
|`systemd_Service_User`|String|| [Service]User
|`systemd_Service_Group`|String|| [Service]Group
|`systemd_Service_WorkingDirectory`|String|| [Service]WorkingDirectory



### [Install]

|name                |type    |default|description
|--------------------|--------|-------|-------------
|`systemd_Install_WantedBy`|String|[Install]WantedBy "multi-user.target"|[Install]WantedBy
|`systemd_Install_RequiredBy`|String||[Install]RequiredBy
|`systemd_Install_Also`|String||[Install]Also
|`systemd_Install_Alias`|String||[Install]Alias


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