# Configuración de Vagrant para Ruby on Rails con Passenger.

Configuración mínima para ejecutar una aplicación Ruby on Rails usando Apache y Passenger en modo de producción.

1. Instalar [Vagrant](https://https://www.vagrantup.com/intro/getting-started/install.html).
1. Clonar este repositorio.
1. `cd aqua-copper`
1. `vagrant up`
1. `vagrant ssh`
1. `cd /vagrant`
1. `EDITOR=nano bin/rails credentials:edit`
1. `sudo systemctl restart apache2`
1. Dirigir un navegador a: http://localhost:8000
1. Se muestra el mensaje: "Welcome#index"
