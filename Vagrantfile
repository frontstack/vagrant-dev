$script = <<SCRIPT
echo 'FrontStack provision script'
hostname frontstack-dev
bash /home/vagrant/scripts/setup.sh
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "frontstack-dev"
  # configure your box image
  # OS release info: https://gist.github.com/casr/e89d304aa46918bbae49
  config.vm.box_url = "http://sourceforge.net/projects/frontstack/files/images/centos65-x86_64-20131219.box/download"
  #config.vm.box_url = "http://nitron-vagrant.s3-website-us-east-1.amazonaws.com/vagrant_ubuntu_12.04.3_amd64_virtualbox.box"

  # port to fordward
  config.vm.network :forwarded_port, guest: 3000, host: 3000
  config.vm.network :forwarded_port, guest: 3001, host: 3001
  config.vm.network :forwarded_port, guest: 3002, host: 3002
  config.vm.network :forwarded_port, guest: 3003, host: 3003
  config.vm.network :forwarded_port, guest: 3010, host: 3010
  config.vm.network :forwarded_port, guest: 3011, host: 3011
  config.vm.network :forwarded_port, guest: 3443, host: 3443
  # livereload
  config.vm.network :forwarded_port, guest: 35729, host: 35729

  config.ssh.forward_agent = true

  config.vm.provider :virtualbox do |v|
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--memory", 768]
    v.customize ["modifyvm", :id, "--name", "FrontStack VM"]
    v.customize ["modifyvm", :id, "--ioapic", "on" ]
    v.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
    v.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/frontstack-env", "1"]
  end

  config.vm.synced_folder "../frontstack-env-x64", "/home/vagrant/frontstack-dev/", id: "frontstack-env"
  config.vm.synced_folder "../vagrant/scripts/", "/home/vagrant/scripts/", id: "frontstack-scripts"

  config.vm.provision "shell", inline: $script
  #config.vm.provision "shell" do |s|
  #  s.path = "../vagrant/scripts/setup.sh"
  #  s.args = "'/home/vagrant/scripts/setup.ini'"
  #end
end
