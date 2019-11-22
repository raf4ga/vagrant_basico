############# Shell para los aprovisionadores  ###############
$script_inicial = <<SCRIPT_INICIAL
### config de hosts
cat <<EOF>> /etc/hosts

192.168.121.100   utility.lab.example.com 	utility
192.168.121.101   tower.lab.example.com 	tower
192.168.121.111   servera.lab.example.com   servera
192.168.121.112   serverb.lab.example.com   serverb
192.168.121.113   serverc.lab.example.com   serverc
192.168.121.114   serverd.lab.example.com   serverd
192.168.121.115   servere.lab.example.com   servere
192.168.121.116   serverf.lab.example.com   serverf
EOF
SCRIPT_INICIAL

############# Shell para el repo  ###############
$script_repos = <<SCRIPT_REPOS
# Eliminamos los repositorios que trae redhat por defecto
  rm -rf /etc/yum.repos.d/*.repo

# config de repo LOCAL
cat > /etc/yum.repos.d/local.repo <<EOF
[local_repo]
name="Local repo"
baseurl=file:///mnt/iso
enable=1
gpgcheck=0

[local_repo_ha]
name="Local repo ha"
baseurl=file:///mnt/iso/addons/HighAvailability
enable=1
gpgcheck=0

[local_repo_stg]
name="Local repo storage"
baseurl=file:///mnt/iso/addons/ResilientStorage
enable=1
gpgcheck=0
EOF

# Se agrega permanentemente la iso de rhel76 a /mnt/iso
cat << EOF >> /etc/fstab
/dev/sr0  /mnt/iso  iso9660 defaults 0 0
EOF
# Se monta la ISO de rhel76 para repositorio local desde el fstab
mount -a

SCRIPT_REPOS

############# Shell para configurar la relación de confianza  ###############
$script_SSH = <<SCRIPT_SSH

# Se debe generar llave SSH en los nodos y se envían localhost y entre todos los nodos

# si se quiere crear en cada nodo uno por uno
  # ssh-keygen
  # ssh-copy-id localhost
  # ssh-copy-id nodo2
  # ....

# Se copia la llave privada a todos los nodos
  cat > /home/vagrant/.ssh/id_rsa <<EOF
-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEAyq6GKwlqEodqSeU3+j5dfpWgP0X2tkDeNfIhxXPbj4ptgMSF
k3dXjDYQrnQiu6CHjgQVJ6a/5zECCHtuzVFTVYkTHRcBXIG07FhvfSjVTpqLuetL
9YlRsUm4nKZU1tm35FBe9f9qZf92Q9yK/B9TGazX6xTVflbj6rokXqyMIqCbWD1U
8NqTqHKv7n8IGMk8GC/PU4Rsc2DWUK1z01OyCB7N+vg7xs2WJOR3GeS4nXk9zTV9
FF0kZK4HY06tRxqqPffeoXxdb4RyjmcJshrTT5iJFxQUiBqW5a2zKVHSJYjtwCW4
Csqke4EmNAb3Hx7tTFxNghLaF0OoBR/OCm41DwIDAQABAoIBADfLTWHhiJKrNmY7
NGqt6lzjYaapYt4PA1zEV+mcGC/ugnB1KPRMYQxXAcaUb89IxKgilZRBwggppI6j
NABPR+p+/oT+hUBq8FwziBVjPT0TLC21CUcBUzzDt49f9nDipE20lj+P3UFQzsSl
nJkFIoIp45JyPMc3siw2q7ZoN3d8UxlyvA5U8i++WqLdQ3cOK7YN28lpAIxPN2YM
nqubCnCrbpJrjqW1W3yBR+remUvGFFODp0bRPl8vhJxIV23YRB/vgpPPcl4iw4l5
Yenxxj+mgnA1NFblguMGh7zaaQjV6IuQyOEKuo8GKnIsU/QFAU86Mu7rtk/If6E9
sbXw2mkCgYEA9oax3spWfofukCdkWFx4OMlg9jRMMDG8OD7tfENiQ5qgQ88MA5Xu
QM2YPdlx7QTinI9bOsJQQE1zjVW8ofpE3YzspBWsQPGF438NfP8tvBwwg2hKhmyg
JMJfU/KWahaZv409dVgW8lr11yxphmvZ7oeeOo+Ia0JTDc9evIzHY/MCgYEA0nh9
xnqBhV+gB8BLZU4YL4jZzhQRxGPQzxd32AAwdlXpmV79h7xYSQpSIoR0Cqo0+TmK
BKT/RBfwgflLNlXg4d/OBTdIidhwXdFQDRIAvauykx4VcvmNaBkZAc94VRjeN9dd
EMQpPIZVDdYm94q+ZjlKhfu2Y9PdNo7ZFAzZHXUCgYBb4qprWslQUgQGMNiC4rxg
lhaQzb9T+0WnRTUpKsh2YCy5+XMF5x0thDPpYaHH8Rkxt3EOfpyAyx11oW40hV6j
oUIWiolwj1UTDSkO3OHEClG+uOGGJvitmtEDLhkII7Jcph0xHos2+9ZDxCb01kAd
WukL9LGpIMhqDk/GQUaUJwKBgHWwFnRzcBVKIUv0RLSC9Jcv6MqJAl5UiiAiuUq4
4GBrLdIrAY1yzdMZyE+wzMph3nk1qW1rbal/0WZ8JYhegP8MjEDyZsddlYeAUUjd
tjhY1+PXwJqn3GBHGGqgvmKnIysKa+nCJmTHoKu6AdQNauXyRy+gTp6Hi3zEZ7IE
dSs5AoGBANxJxUMubhaS6ijzvLthKkh0SHY/MJGp5kxbp+p8xQFREDs0ddVAIuoW
FbqkGzf1ACummgodHuUhnyhIdx4eHJSmr041uq+H80uMroEM5ux0BSQyQGj9S2yF
+hSQsy5UZHAsZqhgnx6WMfdkx4JN8StJr96iCXDp7A8qNbmV7FPf
-----END RSA PRIVATE KEY-----
EOF

# Se copia la llave publica a todos los nodos
  cat >> /home/vagrant/.ssh/id_rsa.pub <<EOF
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDKroYrCWoSh2pJ5Tf6Pl1+laA/Rfa2QN418iHFc9uPim2AxIWTd1eMNhCudCK7oIeOBBUnpr/nMQIIe27NUVNViRMdFwFcgbTsWG99KNVOmou560v1iVGxSbicplTW2bfkUF71/2pl/3ZD3Ir8H1MZrNfrFNV+VuPquiRerIwioJtYPVTw2pOocq/ufwgYyTwYL89ThGxzYNZQrXPTU7IIHs36+DvGzZYk5HcZ5LideT3NNX0UXSRkrgdjTq1HGqo9996hfF1vhHKOZwmyGtNPmIkXFBSIGpblrbMpUdIliO3AJbgKyqR7gSY0BvcfHu1MXE2CEtoXQ6gFH84KbjUP vagrant@utility.lab.example.com
EOF

# Se crea la relacion de confianza con las llaves previamente creadas
cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys

# Se asignan permisos a los archivos
chmod 600 /home/vagrant/.ssh/id_rsa  /home/vagrant/.ssh/authorized_keys
chmod 644 /home/vagrant/.ssh/id_rsa.pub
chown vagrant:vagrant /home/vagrant/.ssh/id_rsa  /home/vagrant/.ssh/authorized_keys /home/vagrant/.ssh/id_rsa.pub

SCRIPT_SSH



############# definición de las VMs

Vagrant.configure("2") do |config|
    # Crea una llave por defecto
    config.ssh.insert_key = false

	config.vm.define :utility do |utility|
		#se define en que box estará basada
    	utility.vm.box = "rhel75"
    	#asigna una IP especifica
    	utility.vm.network :private_network,:ip => "192.168.121.100"
    	#se define el nombre del host de la vm
	    utility.vm.hostname = "utility.lab.example.com"
	    utility.vm.provider :libvirt do |libvirt|
	    	#define la cantidad de memoria RAM
	    	libvirt.memory = 1024
	    	#define la cantidad de CPUs
	      	libvirt.cpus = 2
	      	#define personalizadamente como estará distribuida la CPU
			libvirt.cputopology :sockets => '1', :cores => '2', :threads => '1'
			libvirt.storage :file, :device => :cdrom, :path => '/home/raf4ga/ISOs/rhel-server-7.5-x86_64-dvd.iso'  
	    end
	end

	config.vm.define :tower do |tower|
		#se define en que box estará basada
    	tower.vm.box = "rhel75"
    	#asigna una IP especifica
    	tower.vm.network :private_network,:ip => "192.168.121.101"
    	#se define el nombre del host de la vm
	    tower.vm.hostname = "tower.lab.example.com"
	    tower.vm.provider :libvirt do |libvirt|
	    	#define la cantidad de memoria RAM
	    	libvirt.memory = 1024
	    	#define la cantidad de CPUs
	      	libvirt.cpus = 2
	      	#define personalizadamente como estará distribuida la CPU
			libvirt.cputopology :sockets => '1', :cores => '2', :threads => '1'
			libvirt.storage :file, :device => :cdrom, :path => '/home/raf4ga/ISOs/rhel-server-7.5-x86_64-dvd.iso'
	    end
	end

	config.vm.define :servera do |servera|
		#se define en que box estará basada
    	servera.vm.box = "rhel75"
    	#asigna una IP especifica
    	servera.vm.network :private_network,:ip => "192.168.121.111"
    	#se define el nombre del host de la vm
	    servera.vm.hostname = "servera.lab.example.com"
	    servera.vm.provider :libvirt do |libvirt|
	    	#define la cantidad de memoria RAM
	    	libvirt.memory = 512
	    	#define la cantidad de CPUs
	      	libvirt.cpus = 2
	      	#define personalizadamente como estará distribuida la CPU
			libvirt.cputopology :sockets => '1', :cores => '2', :threads => '1'
			libvirt.storage :file, :device => :cdrom, :path => '/home/raf4ga/ISOs/rhel-server-7.5-x86_64-dvd.iso'
	    end
  	end

	config.vm.define :serverb do |serverb|
		#se define en que box estará basada
    	serverb.vm.box = "rhel75"
    	#asigna una IP especifica
    	serverb.vm.network :private_network,:ip => "192.168.121.112"
    	#se define el nombre del host de la vm
	    serverb.vm.hostname = "serverb.lab.example.com"
	    serverb.vm.provider :libvirt do |libvirt|
	    	#define la cantidad de memoria RAM
	    	libvirt.memory = 512
	    	#define la cantidad de CPUs
	      	libvirt.cpus = 2
	      	#define personalizadamente como estará distribuida la CPU
			libvirt.cputopology :sockets => '1', :cores => '2', :threads => '1'
			libvirt.storage :file, :device => :cdrom, :path => '/home/raf4ga/ISOs/rhel-server-7.5-x86_64-dvd.iso'
	    end
  	end

	config.vm.define :serverc do |serverc|
		#se define en que box estará basada
    	serverc.vm.box = "rhel75"
    	#asigna una IP especifica
    	serverc.vm.network :private_network,:ip => "192.168.121.113"
    	#se define el nombre del host de la vm
	    serverc.vm.hostname = "serverc.lab.example.com"
	    serverc.vm.provider :libvirt do |libvirt|
	    	#define la cantidad de memoria RAM
	    	libvirt.memory = 512
	    	#define la cantidad de CPUs
	      	libvirt.cpus = 2
	      	#define personalizadamente como estará distribuida la CPU
			libvirt.cputopology :sockets => '1', :cores => '2', :threads => '1'
			libvirt.storage :file, :device => :cdrom, :path => '/home/raf4ga/ISOs/rhel-server-7.5-x86_64-dvd.iso'
	    end
	end

	config.vm.define :serverd do |serverd|
		#se define en que box estará basada
    	serverd.vm.box = "rhel75"
    	#asigna una IP especifica
    	serverd.vm.network :private_network,:ip => "192.168.121.114"
    	#se define el nombre del host de la vm
	    serverd.vm.hostname = "serverd.lab.example.com"
	    serverd.vm.provider :libvirt do |libvirt|
	    	#define la cantidad de memoria RAM
	    	libvirt.memory = 512
	    	#define la cantidad de CPUs
	      	libvirt.cpus = 2
	      	#define personalizadamente como estará distribuida la CPU
			libvirt.cputopology :sockets => '1', :cores => '2', :threads => '1'
			libvirt.storage :file, :device => :cdrom, :path => '/home/raf4ga/ISOs/rhel-server-7.5-x86_64-dvd.iso'  
	    end
	end

	config.vm.define :servere do |servere|
		#se define en que box estará basada
    	servere.vm.box = "rhel75"
    	#asigna una IP especifica
    	servere.vm.network :private_network,:ip => "192.168.121.115"
    	#se define el nombre del host de la vm
	    servere.vm.hostname = "servere.lab.example.com"
	    servere.vm.provider :libvirt do |libvirt|
	    	#define la cantidad de memoria RAM
	    	libvirt.memory = 512
	    	#define la cantidad de CPUs
	      	libvirt.cpus = 2
	      	#define personalizadamente como estará distribuida la CPU
			libvirt.cputopology :sockets => '1', :cores => '2', :threads => '1'
			libvirt.storage :file, :device => :cdrom, :path => '/home/raf4ga/ISOs/rhel-server-7.5-x86_64-dvd.iso'
	    end
	end

	config.vm.define :serverf do |serverf|
		#se define en que box estará basada
    	serverf.vm.box = "rhel75"
    	#asigna una IP especifica
    	serverf.vm.network :private_network,:ip => "192.168.121.116"
    	#se define el nombre del host de la vm
	    serverf.vm.hostname = "serverf.lab.example.com"
	    serverf.vm.provider :libvirt do |libvirt|
	    	#define la cantidad de memoria RAM
	    	libvirt.memory = 512
	    	#define la cantidad de CPUs
	      	libvirt.cpus = 2
	      	#define personalizadamente como estará distribuida la CPU
			libvirt.cputopology :sockets => '1', :cores => '2', :threads => '1'
			libvirt.storage :file, :device => :cdrom, :path => '/home/raf4ga/ISOs/rhel-server-7.5-x86_64-dvd.iso'  
	    end
	end

	config.vm.provision "shell", inline: $script_inicial
	config.vm.provision "shell", inline: $script_repos
	config.vm.provision "shell", inline: $script_SSH
end

# echo "export VAGRANT_DEFAULT_PROVIDER=libvirt" > ~/.bashrc 
