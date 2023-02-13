Vagrant.configure("2") do |config|
  config.vm.box = "almalinux/8"
    config.vm.box_check_update = false
    config.vm.network "forwarded_port", guest: 9090, host: 9090
    config.vm.network "forwarded_port", guest: 3000, host: 3000
    config.vm.provision "shell", inline: <<-SHELL
      sudo dnf install -y epel-release
      #sudo dnf install -y wget screen
      #curl -s https://api.github.com/repos/prometheus/prometheus/releases/latest | grep browser_download_url | grep linux-amd64 | cut -d '"' -f 4 | wget -qi -

      #установка сервиса (сервера) prometheus
      tar xvf /vagrant/prometheus-*.tar.gz -C /home/vagrant
      mv /home/vagrant/prometheus-*/ /home/vagrant/prometheus
      sudo groupadd --system prometheus
      sudo useradd --system -g prometheus -s /bin/false prometheus
      sudo mkdir /etc/prometheus /var/lib/prometheus
      sudo cp /home/vagrant/prometheus/prometheus /home/vagrant/prometheus/promtool /usr/local/bin
      sudo cp -r /home/vagrant/prometheus/console* /etc/prometheus
      sudo cp /vagrant/prometheus.yml /etc/prometheus/prometheus.yml
      sudo chown -R prometheus:prometheus /var/lib/prometheus /etc/prometheus
      sudo chown prometheus:prometheus /usr/local/bin/prometheus /usr/local/bin/promtool
      sudo cp /vagrant/prometheus.service /etc/systemd/system/prometheus.service

      #установка node_explorer
      tar xvf /vagrant/node_exporter-*.tar.gz -C /home/vagrant
      mv /home/vagrant/node_exporter-*/ /home/vagrant/node_exporter
      sudo cp /home/vagrant/node_exporter/node_exporter /usr/local/bin
      sudo chown -R prometheus:prometheus /usr/local/bin/node_exporter
      sudo cp /vagrant/node_exporter.service /etc/systemd/system/node_exporter.service

      #grafana
      #sudo cp /vagrant/grafana.repo /etc/yum.repos.d/grafana.repo
      #sudo dnf -y install grafana
      sudo dnf install -y fontconfig urw-fonts sysbench
      sudo rpm -i /vagrant/grafana-9.3.6-1.x86_64.rpm
      sudo cp /vagrant/grafana-prometheus.yml /etc/grafana/provisioning/datasources/prometheus.yml
      sudo chown grafana:grafana /etc/grafana/provisioning/datasources/prometheus.yml

      #запуск
      sudo systemctl daemon-reload
      sudo systemctl enable prometheus.service --now
      sudo systemctl enable node_exporter.service --now
      sudo systemctl enable grafana-server.service --now
    SHELL
end
