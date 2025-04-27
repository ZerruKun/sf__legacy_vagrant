# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/lucid64" # Или другой образ с Ubuntu 10.04
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update -y
    sudo apt-get install -y postgresql-8.4 postgresql-client-8.4
    sudo -u postgres createuser -s vagrant
    sudo -u postgres psql -c "ALTER USER postgres PASSWORD 'postgres';"
    sudo sed -i 's/^\(local.*\)peer/\1md5/' /etc/postgresql/8.4/main/pg_hba.conf
    sudo sed -i 's/^\(host.*\)md5/\1trust/' /etc/postgresql/8.4/main/pg_hba.conf
    sudo service postgresql restart
    sudo service postgresql status
  SHELL
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.cpus = 1
  end
end
