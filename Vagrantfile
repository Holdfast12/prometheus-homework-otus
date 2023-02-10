Vagrant.configure("2") do |config|
  config.vm.box = "almalinux/8"
    config.vm.box_check_update = false
    config.vm.network "forwarded_port", guest: 9090, host: 9090
    config.vm.provision "shell", inline: <<-SHELL
      sudo dnf install -y epel-release
      sudo dnf install -y wget screen
      cd /vagrant/
      curl -s https://api.github.com/repos/prometheus/prometheus/releases/latest | grep browser_download_url | grep linux-amd64 | cut -d '"' -f 4 | wget -qi -
      tar xvf prometheus-*.tar.gz
      mv prometheus-*/ prometheus
      sudo chown -R vagrant:vagrant ./prometheus
      #/vagrant/prometheus/prometheus --config.file "/vagrant/prometheus/prometheus.yml"
    SHELL
end
