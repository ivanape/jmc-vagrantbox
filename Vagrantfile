Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = true
    vb.memory = 4096
    vb.name = "JMC VM"
  end

  # https://askubuntu.com/questions/1067929/on-18-04-package-virtualbox-guest-utils-does-not-exist
  config.vm.provision "shell", inline: "sudo apt-add-repository multiverse && sudo apt-get update"

  # Install xfce and virtualbox additions.
  config.vm.provision "shell", inline: "sudo apt-get install -y xfce4 virtualbox-guest-dkms virtualbox-guest-utils virtualbox-guest-x11"
  config.vm.provision "shell", inline: "sudo sed -i 's/allowed_users=.*$/allowed_users=anybody/' /etc/X11/Xwrapper.config"
  config.vm.provision "shell", inline: "sudo apt-get install -y lightdm lightdm-gtk-greeter"
  config.vm.provision "shell", inline: "sudo apt update && sudo apt -y install openjdk-11-jre-headless"
  config.vm.provision "shell", inline: "sudo apt-get install -y xfce4-whiskermenu-plugin"
  config.vm.provision "shell", inline: "sudo apt-get install -y xfce4-whiskermenu-plugin"

  # Copy JMC local build
  config.vm.provision "file", source: "./linux/gtk/x86_64", destination: "/home/vagrant/jmc-7.1.0"
  config.vm.provision "shell", inline: "chmod +x /home/vagrant/jmc-7.1.0/jmc"

  # vagrant plugin install vagrant-reload
  config.vm.provision :reload

  #Generate box with
  #vagrant package --output jmc.box

  #Publish on vagrant cloud
  #vagrant cloud publish programwar/jmc 0.0.1 virtualbox jmc.box
end
