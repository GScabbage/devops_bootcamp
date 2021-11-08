
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

# runs the provision file at boot, which updates and upgrades patchs and install nginx in this case
 config.vm.provision :shell, path: "provision.sh", run: 'always'

end
