Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt update
    sudo apt install -y postgresql
  SHELL
end