Vagrant.configure("2") do |config|
  config.vm.box = "almalinux/8"
    config.vm.box_check_update = false
    config.vm.network "forwarded_port", guest: 9090, host: 9090
    config.vm.provision "shell", inline: <<-SHELL
      sudo dnf install -y epel-release
      sudo dnf install -y wget screen
      wget https://github.com/prometheus/prometheus/releases/download/v1.8.0/prometheus-1.8.0.darwin-amd64.tar.gz
      tar xvf prometheus-*.tar.gz
      sudo chown vagrant:vagrant prometheus-*/
    SHELL
end
