# 开发前



## vagrant配置
```
Vagrant.configure("2") do |config|
  config.vm.define "master" do |master|
    master.vm.box = "precise64"
    master.vm.hostname = 'master'
    master.vm.box_url = "D:/soft/virtualbox/precise-server-cloudimg-amd64-vagrant-disk1.box"
    master.vm.synced_folder "D:/vagrant/shared", "/vagrant_data",id: "vagrant-root",
      owner: "vagrant",
      group: "www-data",
      mount_options: ["dmode=775,fmode=664"]
    master.vm.network :private_network, ip: "192.168.56.100"

    master.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "master"]
    end
  end

  config.vm.define "web" do |web|
    web.vm.box = "precise64"
    web.vm.hostname = 'web'
    web.vm.box_url = "D:/soft/virtualbox/precise-server-cloudimg-amd64-vagrant-disk1.box"

    web.vm.network :private_network, ip: "192.168.56.101"

    web.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "web"]
    end
  end

  config.vm.define "api" do |api|
    api.vm.box = "precise64"
    api.vm.hostname = 'db'
    api.vm.box_url = "D:/soft/virtualbox/precise-server-cloudimg-amd64-vagrant-disk1.box"

    api.vm.network :private_network, ip: "192.168.56.102"

    api.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "api"]
    end
  end

  config.vm.define "daemon" do |daemon|
    daemon.vm.box = "precise64"
    daemon.vm.hostname = 'daemon'
    daemon.vm.box_url = "D:/soft/virtualbox/precise-server-cloudimg-amd64-vagrant-disk1.box"

    daemon.vm.network :private_network, ip: "192.168.56.103"

    daemon.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "daemon"]
    end
  end

end
```

## 参考
- [vagrant权限问题](http://jeremykendall.net/2013/08/09/vagrant-synced-folders-permissions/)
