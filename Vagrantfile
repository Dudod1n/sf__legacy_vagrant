Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.provision "shell", inline: <<-SHELL
echo "Install deps"
apt install -y gnupg gnupg2 gnupg1

echo "Create the file repository configuration"
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'

echo "Import the repository signing key"
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -

echo "Update the package lists"
sudo apt update

echo "Install PostgreSQL 8.4"    
apt install -y postgresql-client-8.4 postgresql-8.4

    echo "Configuring and restarting PostgreSQL"
    echo 'listen_addresses = '"'"'*'"'" >> /etc/postgresql/8.4/main/postgresql.conf
    echo 'host    all             all             10.0.2.0/24            md5' >> /etc/postgresql/8.4/main/pg_hba.conf
    systemctl restart postgresql
    echo "Creating vagrant user and database"
    echo "CREATE ROLE vagrant CREATEDB CREATEROLE CREATEUSER LOGIN UNENCRYPTED PASSWORD 'vagrant'" | sudo -u postgres psql -a -f -
    echo "CREATE DATABASE vagrant OWNER vagrant" | sudo -u postgres psql -a -f -
    echo "Preparing for packaging"
  SHELL
end