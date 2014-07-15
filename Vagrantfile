# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
	config.vm.define "virtualbox" do |vbox|
		vbox.vm.box = "hashicorp/precise64"
		vbox.vm.box_url = "https://vagrantcloud.com/hashicorp/precise64"
		config.vm.network :forwarded_port, host: 4567, guest: 80
	end

	config.vm.define "openstack", autostart: false do |osConfig|
		require 'vagrant-openstack-plugin'

		osConfig.ssh.private_key_path = "keypair-name.cer"

		osConfig.vm.box = "dummy"
		osConfig.vm.box_url = "https://github.com/cloudbau/vagrant-openstack-plugin/raw/master/dummy.box"

		osConfig.vm.provider :openstack do |os|
			os.username     = "#{ENV['OS_USERNAME']}"
			os.api_key      = "#{ENV['OS_PASSWORD']}"
			os.flavor       = /m1.small/                # Regex or String
			os.image        = /xdata-centos-base/                 # Regex or String
			os.endpoint     = "#{ENV['OS_AUTH_URL']}/tokens"
			os.keypair_name = "KEYPAIR-NAME"      # as stored in Nova
			os.ssh_username = "cloud-user"           # login for the VM
			os.floating_ip = "auto"
			os.networks = []
			os.server_name = "testing_snapshot"
		end

		osConfig.ssh.pty = true

		osConfig.vm.synced_folder ".", "/vagrant", disabled: true

		osConfig.vm.network "forwarded_port", host: 4567, guest: 8080
	end
end

