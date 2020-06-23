# Install required plugins
required_plugins = ["vagrant-hostsupdater"]
required_plugins.each do |plugin|
    exec "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/xenial64"
    config.vm.network "private_network", ip: "192.168.10.150"
#    config.vm.network "forwarded_port", guest: 3000, host: 3000
#    config.vm.network "forwarded_port", guest: 27017, host: 27017, id: "mongodb"
    config.hostsupdater.aliases = ["database.local"]
    config.vm.provision "shell", path: "environment/db/provision.sh", privileged: false
end
