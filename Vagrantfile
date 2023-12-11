$setup_postgres_db = <<-'SCRIPT' 
sudo echo deb http://apt.postgresql.org/pub/repos/apt/ focal-pgdg main > /etc/apt/sources.list.d/pgdg.list
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo apt-get update
sudo DEBIAN_FRONTEND=noninteractive apt-get install postgresql-8.4 -y
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.hostname = "sf-postgresql"
  config.vm.provision "shell", inline: $setup_postgres_db
end