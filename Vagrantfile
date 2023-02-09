Vagrant.configure("2") do |config|
  config.vm.box = "almalinux/8"
    config.vm.box_check_update = false
    config.vm.network "forwarded_port", guest: 9090, host: 9090
    config.vm.provision "shell", inline: <<-SHELL
      sudo dnf install -y wget
      curl -s https://api.github.com/repos/prometheus/prometheus/releases/latest | grep browser_download_url | grep linux-amd64 | cut -d '"' -f 4 | wget -qi -
      tar xvf prometheus-*.tar.gz
      cd prometheus-*/
    SHELL
end
