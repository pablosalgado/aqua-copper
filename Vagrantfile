$system = <<-SCRIPT

apt-get update

export DEBIAN_FRONTEND=noninteractive

# ------------------------------------------------------------------------------
# Instalación y configuración del servidor Apache
# ------------------------------------------------------------------------------
apt-get install -y apache2

cat > /etc/apache2/sites-available/000-default.conf << EOF
<VirtualHost *:80>
        ServerAdmin webmaster@localhost
        DocumentRoot /vagrant/public/
        RailsEnv production
        PassengerRuby /usr/bin/ruby

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        <Directory "/vagrant/public">
                Options FollowSymLinks
                Require all granted
        </Directory>
</VirtualHost>
EOF

systemctl restart apache2

# ------------------------------------------------------------------------------
# Install Passenger
# ------------------------------------------------------------------------------
apt-get install -y libapache2-mod-passenger

# ------------------------------------------------------------------------------
# Instalación de Ruby y dependencias mínimas para la aplicación de Ruby on Rails
# ------------------------------------------------------------------------------
apt-get install -y build-essential ruby ruby-dev libsqlite3-dev

# ------------------------------------------------------------------------------
# Instalación de Bundler
# ------------------------------------------------------------------------------
gem install bundler:2.0.2

SCRIPT

$user = <<-SCRIPT
  cd /vagrant

  bundle install --deployment

  rm ./config/credentials.yml.enc
  rm ./config/master.key
  EDITOR=vim bin/rails credentials:edit

  RAILS_ENV=production bin/bundle exec rake assets:precompile
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-18.04"
  config.vm.provision "shell", inline: $system
  config.vm.provision "shell", inline: $user, privileged: false
  config.vm.network :forwarded_port, guest: 80, host: 8000
end
