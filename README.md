# DevOps Intro
## Life Before DevOps
- The Waterfall life cycle, which was very hard to return to previous points of to fix things
- Developers used to make software and give it to Operations and it wouldn't work because environments were different and the only thing Developers could say was "It was working on my machine"
### why DevOps
- **DevOps Introduction**
- Devops is the merging of the development and operations team
- A collaboration of Development and Operations
- A culture which promotes collaboration between Development and Operations team to deploy code to production faster in an automated and repeatable way
- A practice of development and operation engineers taking part together in the whole service lifecycle
- An approach through which superior quality software can be developed quickly and with more reliability
- An alignment of development and IT operations with better communication and collaboration
#### Key Pillars of DevOps
- Ease of Use
- Robustness
- Cost Effective
- Flexibility
##### Monolith Architecture
- Everything works in the same package
- Bad for agile because you have to finish the entire app before you can deliver anything
- Fine for small projects but still not great

### Development Environment
![](images/dev-env.png)

- Create `vagrantfile` in the current location
```
Vagrant.configure("2") do |config|

 config.vm.box = "ubuntu/xenial64"
# creating a virtual machine ubuntu

# assign private ip to our VM
 config.vm.network "private_network", ip: "192.168.10.100"

# ensure to install hostsupdater plugin on our localhost
 config.hostsupdater.aliases = ["development.local"]

 # Sync folder from OS to VM
 # "." is current location - to our vm
  config.vm.synced_folder ".", "/home/vagrant/app"

end
```
- Create `provision.sh`, updates system, upgrades packages and installs nginx
```
#!/bin/bash
# update system
sudo apt-get update -y

# upgrade packages
sudo apt-get upgrade -y

# install nginx
sudo apt install nginx -y

#load nginx on 192.168.10.100
```
- Use `sudo chmod +x provision.sh` to make it executable
- Add the below line into the `vagrantfile` above end, this will run the provision.sh file on use of `vagrant up`
- It has `run: always` at the end so that it reruns everytime it is reloaded

```
# runs the provision file at boot, which updates and upgrades patchs and install nginx in this case
 config.vm.provision :shell, path: "provision.sh", run: 'always'
```

- You should then be able to connect on your localhost at `192.168.10.100`
- If not the `vagrant ssh` into your vm and check nginx status with `systemctl status nginx`

- Vagrant Commands

```
Common commands:
     autocomplete    manages autocomplete installation on host
     box             manages boxes: installation, removal, etc.
     cloud           manages everything related to Vagrant Cloud
     destroy         stops and deletes all traces of the vagrant machine
     global-status   outputs status Vagrant environments for this user
     halt            stops the vagrant machine
     help            shows the help for a subcommand
     hostsupdater
     init            initializes a new Vagrant environment by creating a Vagrantfile
     login
     package         packages a running vagrant environment into a box
     plugin          manages plugins: install, uninstall, update, etc.
     port            displays information about guest port mappings
     powershell      connects to machine via powershell remoting
     provision       provisions the vagrant machine
     push            deploys code in this environment to a configured destination
     rdp             connects to machine via RDP
     reload          restarts vagrant machine, loads new Vagrantfile configuration
     resume          resume a suspended vagrant machine
     snapshot        manages snapshots: saving, restoring, etc.
     ssh             connects to machine via SSH
     ssh-config      outputs OpenSSH valid configuration to connect to the machine
     status          outputs status of the vagrant machine
     suspend         suspends the machine
     up              starts and provisions the vagrant environment
     upload          upload to machine via communicator
     validate        validates the Vagrantfile
     version         prints current and latest Vagrant version
     winrm           executes commands on a machine via WinRM
     winrm-config    outputs WinRM configuration to connect to the machine

```
