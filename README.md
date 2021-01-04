![](https://img.shields.io/badge/Ansible-jenkins-green.svg?logo=angular&style=for-the-badge)

>__Please note that the original design goal of this role was more concerned with the initial installation and bootstrapping environment, which currently does not involve performing continuous maintenance, and therefore are only suitable for testing and development purposes, should not be used in production environments. The author does not guarantee the accuracy, completeness, reliability, and availability of the role content. Under no circumstances will the author be held responsible or liable in any way for any claims, damages, losses, expenses, costs or liabilities whatsoever, including, without limitation, any direct or indirect damages for loss of profits, business interruption or loss of information..__

>__请注意，此角色的最初设计目标更关注初始安装和引导环境，目前不涉及执行连续维护，因此仅适用于测试和开发目的，不应在生产环境中使用。作者不对角色内容之准确性、完整性、可靠性、可用性做保证。在任何情况下，作者均不对任何索赔，损害，损失，费用，成本或负债承担任何责任，包括但不限于因利润损失，业务中断或信息丢失而造成的任何直接或间接损害。__
___

<p><img src="https://raw.githubusercontent.com/goldstrike77/goldstrike77.github.io/master/img/logo/logo_jenkins.png" align="right" /></p>

__Table of Contents__

- [Overview](#overview)
- [Requirements](#requirements)
  * [Operating systems](#operating-systems)
  * [jenkins Versions](#jenkins-versions)
- [ Role variables](#Role-variables)
  * [Main Configuration](#Main-parameters)
  * [Other Configuration](#Other-parameters)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)
  * [Hosts inventory file](#Hosts-inventory-file)
  * [Vars in role configuration](#vars-in-role-configuration)
  * [Combination of group vars and playbook](#combination-of-group-vars-and-playbook)
- [License](#license)
- [Author Information](#author-information)
- [Contributors](#Contributors)

## Overview
Jenkins is a free and open-source automation server. It helps automate the parts of software development related to building, testing, and deploying, facilitating continuous integration and continuous delivery. It is a server-based system that runs in servlet containers.

## Requirements
### Operating systems
This Ansible role installs Jenkins on the Linux operating system, including establishing a filesystem structure and server configuration with some common operational features. This role will work on the following operating systems:

  * CentOS 7

### jenkins versions

The following list of supported the Jenkins releases:

* Jenkins 2.x LTS

## Role variables
### Main parameters #
There are some variables in defaults/main.yml which can (Or needs to) be overridden:
##### General parameters
* `jenkins_is_install`: A boolean to determine whether or not to install the Jenkins.
* `jenkins_version`: Specify the Jenkins version.
* `jenkins_path`: Specify the Jenkins working directory.
* `jenkins_admin_user`: The default administrator username.
* `jenkins_admin_pass`: The password for administrator.
* `jenkins_force_https`: A boolean to determine whether or not to Encrypting HTTP client communications.

##### JVM memory Variables
* `jenkins_jvm_xmx`: Size of the heap in MB.

##### Listen port
* `jenkins_port.http`: http port number.
* `jenkins_port.https`: https port number.
* `jenkins_port.wrapper`: A socket to communicate with its Java component running inside a JVM.
* `jenkins_port.wrapper_jvm`: A socket to communicate with its Java component running inside a JVM.

##### System Variables
* `jenkins_arg.timeout`: Sets the http session timeout value for minutes.
* `jenkins_arg.lc_ctype`: The language of messages.
* `jenkins_arg.timezone`: Default timezone for a single instance of a running JVM.
* `jenkins_arg.user`: Jenkins running user.
* `jenkins_arg.ulimit_core`: The number of core dump launched by systemd.
* `jenkins_arg.ulimit_nofile`: The number of files launched by systemd.
* `jenkins_arg.ulimit_nproc`: The number of processes launched by systemd.
* `jenkins_arg.wrapper_console_format`: Format to use for output to the console.
* `jenkins_arg.wrapper_console_loglevel`: Log level to use for console output.
* `jenkins_arg.wrapper_java_command_loglevel`: Log level to use for Java command.
* `jenkins_arg.wrapper_logfile`: Sets the path to the Wrapper log file.
* `jenkins_arg.wrapper_logfile_format`: Format to use for logging to the log file.
* `jenkins_arg.wrapper_logfile_loglevel`: Filters messages sent to the log file according to their log levels.
* `jenkins_arg.wrapper_logfile_maxfiles`: Controls the maximum number of rolled files.
* `jenkins_arg.wrapper_logfile_maxsize`: Controls the maximum size of rolled files.
* `jenkins_arg.wrapper_syslog_loglevel`: Log level to use for logging to the Event Log on syslog on UNIX systems.
* `jenkins_arg.wrapper_ulimit_loglevel`: Controls at which log level resource limits will be logged.

##### Plugins Variables
* `jenkins_plugins`: Lists the plugins for installs.

##### Service Mesh
* `environments`: Define the service environment.
* `datacenter`: Define the DataCenter.
* `domain`: Define the Domain.
* `customer`: Define the customer name.
* `tags`: Define the service custom label.
* `exporter_is_install`: Whether to install prometheus exporter.
* `consul_public_register`: Whether register a exporter service with public consul client.
* `consul_public_exporter_token`: Public Consul client ACL token.
* `consul_public_http_prot`: The consul Hypertext Transfer Protocol.
* `consul_public_clients`: List of public consul clients.
* `consul_public_http_port`: The consul HTTP API port.

### Other parameters
There are some variables in vars/main.yml:

## Dependencies
- Ansible versions >= 2.8
- Python >= 2.7.5
- [Jenkins](https://github.com/goldstrike77/ansible-role-linux-jenkins.git)

## Example

### Hosts inventory file
See tests/inventory for an example.

### Vars in role configuration
Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: all
  roles:
     - role: ansible-role-linux-jenkins
```

### Combination of group vars and playbook
You can also use the group_vars or the host_vars files for setting the variables needed for this role. File you should change: group_vars/all or host_vars/`group_name`.

```yaml
jenkins_version: '2.263.1'
jenkins_path: '/data'
jenkins_admin_user: 'admin'
jenkins_admin_pass: 'changeme'
jenkins_force_https: true
jenkins_jvm_xmx: '2048'
jenkins_plugins:
  - name: 'ansible'
    version: 'latest'
  - name: 'prometheus'
    version: 'latest'
jenkins_port:
  http: '8080'
  https: '8443'
  wrapper: '35000-35999'
  wrapper_jvm: '36000-36999'
jenkins_arg:
  timeout: '10'
  lc_ctype: 'zh_CN.UTF-8'
  timezone: 'Asia/Shanghai'
  user: 'jenkins'
  ulimit_core: 'unlimited'
  ulimit_nofile: '20480'
  ulimit_nproc: '20480'
  wrapper_console_format: 'PM'
  wrapper_console_loglevel: 'INFO'
  wrapper_java_command_loglevel: 'NONE'
  wrapper_logfile: 'jenkins.out'
  wrapper_logfile_format: 'ZM'
  wrapper_logfile_loglevel: 'INFO'
  wrapper_logfile_maxfiles: '25'
  wrapper_logfile_maxsize: '50m'
  wrapper_syslog_loglevel: 'NONE'
  wrapper_ulimit_loglevel: 'STATUS'
environments: 'prd'
datacenter: 'dc01'
domain: 'local'
customer: 'demo'
tags:
  subscription: 'default'
  owner: 'nobody'
  department: 'Infrastructure'
  organization: 'The Company'
  region: 'China'
exporter_is_install: false
consul_public_register: false
consul_public_exporter_token: '00000000-0000-0000-0000-000000000000'
consul_public_http_prot: 'https'
consul_public_http_port: '8500'
consul_public_clients:
  - '127.0.0.1'
```

## License
![](https://img.shields.io/badge/MIT-purple.svg?style=for-the-badge)

## Author Information
Please send your suggestions to make this role better.

## Contributors
Special thanks to the [Connext Information Technology](http://www.connext.com.cn) for their contributions to this role.
