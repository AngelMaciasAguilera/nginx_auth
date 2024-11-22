Vagrant.configure("2") do |config|
  config.vm.box = "debian/bookworm64"

  config.vm.define "nginxauthmachine" do |nginxauthmachine| 
    nginxauthmachine.vm.hostname = "nginxauthmachine.deaw.test"
    nginxauthmachine.vm.network "private_network", ip:"192.168.57.12"
    nginxauthmachine.vm.provision "shell", name: "Update_machine", inline: <<-SHELL
      apt-get update
      sudo apt-get install -y nginx
      sudo cp -vr /vagrant/.htpasswd /etc/nginx/.htpasswd
      sudo cp -vr  /vagrant/nginxpageauth.org /etc/nginx/sites-available/
      sudo ln -s /etc/nginx/sites-available/nginxpageauth.org /etc/nginx/sites-enabled/
      sudo systemctl restart nginx
      sudo mkdir -p /var/www/deaw/html
      sudo cp -vr /vagrant/html/* /var/www/deaw/html/
      sudo systemctl restart nginx

    SHELL
  end
end
