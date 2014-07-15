Install vagrant-openstack-plugin

```bash
$ vagrant plugin install vagrant-openstack-plugin
```

Download OpenStack RC File from OpenStack dashboard: 

- Access & Security

	- API Access

		- Click Download OpenStack RC File


load environment variables

```bash
$ source downloaded-file.sh
```

Alter `Vagrantfile` to use correct `pem` file and associated KeyPair name

Vagrant up

```bash
$ vagrant up openstack --provider=openstack
```

