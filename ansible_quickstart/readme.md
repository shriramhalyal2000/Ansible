# Ansible playbooks with server configurations.

- no need to write bashscripts for install, update, maintain and destroy tools on servers with ssh and required perms.

- Ansible configuration syntax
  - It is a configuration as a code platform, that bypasses mannualy loggin in servers and mantaining tools version, update/upgrade, and removal or change.
  - setting up the configuratins as the need.

What was before Ansible?
 - s/w development had system admins who  managed server configurations and tools installed on them.
 - the tools were versioned and maintained by the admins over the period of time, and updated with mannually loggin in with remote tolles like winre, ssh on to the servers mannually and installed, updated and removed them.
 - this process is slow and overly complicated as it takes time and effort more along wiwth debugging problem with different os distributions.
 - so admins switched to scripts shell scripts but there were also ubnreliable as different distributions of linux had different package managerse apt, yum etc for centos, debian and ubuntu.
 - configuration management tool puppet, chef, salt and ansible
 - Apart from ansible all are agentic architecture which needs s/w installed on target servers, with profound compledx code/configuration syntax.
 - But ansibl eis agentless architecture which needs none of that. written in yaml and called playbooks.
 - Ansible architedcture:
   - control nodes and managed nodes.
     - machine where ansible installed: controlled node.
     - managed nodes : target nodes on which s/w tool are installed by control node.(any and all vms which need to have tools installed on them.)
       - managed node can be any kind of os/distribution. indiscriminant of os.
       - pre-requisite python installed on them.
  - started as configuration management, now its highly recomended automation platform, can also do provisioning.
  - used for CI/CD deployment

  - sudo apt install ansible -y

  -- passowrd less auth with ansible.
    - ansible Adhoc commands.
    - ansible inventory
    - understanding adhoc commands and usage.
    - understand adhoc comamnds and management tasks.
    - exploring power of adhoc commands for quick tasks.

    - passwordless authntication is key for automation , thought it required one time mannual intervention, but once set up it wont ask repeatedly.
      - ssh-copy-id -f "-o IdentityFile <PATH TO PEM FILE>" ubuntu@<INSTANCE-PUBLIC-IP> to set up passowrd less auth usin gpublic key of remote vm/instances
    - Ansible inventory:
      - to tell ansible its managed nodes, to which all vms it needs to monitor to install/configure tools, it needs check of its inventory.
      file.ini needs to be created to store vm with its ip, that can be used in ansible configuration files to use them as target nodes. and considering passwordless auth is set up for it so ansible can control them. 
      - /etc/ansible/hosts for default hosts for ansible.
  - ansible adhoc commands:
    - $ ansible -i inventory.ini -m ping all
      - pings all hosts within inventory files.
    - $ ansible -i inventory.ini -m shell -a "apt install openjdk" all
    - $ ansible -i inventory.ini -m ping app # db to ping specific set of servers with inventory configured.   
    