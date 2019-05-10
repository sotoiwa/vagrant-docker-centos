# -*- mode: ruby -*-
# vi: set ft=ruby :

# プロビジョニングスクリプト
$configureBox = <<-SHELL

  # パッケージ更新
  yum update -y

  # Dockerの前提パッケージ
  yum install -y yum-utils device-mapper-persistent-data lvm2
  # Dockerのレポジトリ追加
  yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
  # Dockerのインストール
  # VERSION=$(yum list docker-ce --showduplicates | sort -r | grep 17.03 | head -1 | awk '{print $2}')
  # yum install -y --setopt=obsoletes=0 docker-ce-$VERSION docker-ce-selinux-$VERSION
  VERSION=$(yum list docker-ce --showduplicates | sort -r | grep 18.06.1 | head -1 | awk '{print $2}')
  yum install -y docker-ce-$VERSION

  mkdir -p /etc/systemd/system/docker.service.d
  systemctl enable docker
  systemctl daemon-reload
  systemctl restart docker

  # vagrantユーザーをdockerグループに追加
  usermod -aG docker vagrant

SHELL

Vagrant.configure(2) do |config|

  config.vm.box = "centos/7"

  config.vm.network "private_network", ip: "192.168.33.10"

  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end

  # プロビジョニング実行
  s.vm.provision "shell", inline: $configureBox

end
