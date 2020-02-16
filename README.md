<!-- PROJECT LOGO -->
<br />
<p align="center">
  <a href="https://github.com/prominic/Docova-Vagrant/">
    <img src="conf/wiki/images/Prom.jpg" alt="Logo" width="200" height="100">
  </a>

  <h3 align="center">Docova Vagrant Build</h3>

  <p align="center">
    An README to jumpstart your build of the Docova Bundle
    <br />
    <a href="https://github.com/prominic/Docova-Vagrant/"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/prominic/Docova-Vagrant/">View Demo</a>
    ·
    <a href="https://github.com/prominic/Docova-Vagrant/issues">Report Bug</a>
    ·
    <a href="https://github.com/prominic/Docova-Vagrant/issues">Request Feature</a>
  </p>
</p>



<!-- TABLE OF CONTENTS -->
## Table of Contents

* [About the Project](#Docova-Vagrant)
  * [Built With](#built-with)
* [Getting Started](#getting-started)
  * [Prerequisites](#prerequisites)
  * [Installation](#downloading-docova-project-to-a-local-folder)
    * [Mac OS X](https://github.com/prominic/Docova-Vagrant/blob/master/MacMojaveReadme.md) -- Quick Start
    * [Windows](https://github.com/prominic/Docova-Vagrant/blob/master/Win10ReadMe.md) -- Quick Start
* [Rebuilding](#rebuilding-the-project)
* [Roadmap](#roadmap)
* [Contributing](#contributing)
* [License](#license)
* [Contact](#authors)
* [Acknowledgements](#acknowledgments)



# Docova-Vagrant
Primary goal is to use Vagrant on Windows, Mac, and Linux to deploy the latest Docova Bundle in an Ubuntu 18.04 VM, in order to run regression tests and automating installation via API call from Docova Web Services. This uses a Specialized Packer Build that cuts down deployment time.

We will keep the Master branch as the core of the project and any application that we want to Automate/Regression Test we will branch in order to compartmentalize the project for use with mutiple applications.
 
## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. You MUST have the Vagrant, Virtualbox and Git installed on your machine. Please follow the instructions below for setting up your VM with the pre-requistes. 

### Prerequisites

You will need some software on your PC or Mac:

```
git
Vagrant
Virtualbox
```

### Installing

To ease deployment, we have a few handy scripts that will utlize a package manager for each OS to get the pre-requisite software for your host OS. This is NOT required, this is to help you ensure you have all the applications that are neccessary to run this VM.

#### Windows
Powershell has a package manager named Chocalatey which is very similar to SNAP, YUM, or other Package manager, We will utilize that to quickly install Virtualbox, Vagrant and Git.

Powershell
```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
choco install vagrant
choco install virtualbox
choco install git.install
```

For those that need to run this in a Command Prompt, you can use this:

CMD
```bat
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
choco install vagrant
choco install virtualbox
choco install git.install
```

#### Mac
Just like Windows and other Linux repos, there is a similar package manager for Mac OS X, Homebrew, We will utilize that to install the prequsites. You will likley need to allow unauthenticated applications in the Mac OS X Security Settings, there are reports that Mac OS X Mojave will require some additional work to get running correctly. You do NOT have to use these scripts to get the pre-requisites on your Mac, it is recommened, you simply need to make sure you have the 3 applications installed on your Mac.

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew cask install virtualbox
brew cask install vagrant
brew cask install vagrant-manager
brew install git
```

#### CentOS 7
We will utilize YUM and a few other bash commands to get the Virtualbox, Git,  and Vagrant installed.

YUM
```shell
yum -y install gcc dkms make qt libgomp patch kernel-headers kernel-devel binutils glibc-headers glibc-devel font-forge
cd /etc/yum.repo.d/
wget http://download.virtualbox.org/virtualbox/rpm/rhel/virtualbox.repo
yum install -y VirtualBox-5.1
/sbin/rcvboxdrv setup
yum -y install https://releases.hashicorp.com/vagrant/1.9.6/vagrant_1.9.6_x86_64.rpm
sudo yum install git
```

#### Ubuntu
We will utilize APT to get the Virtualbox, Git,  and Vagrant installed.

APT
```shell
sudo apt-get install virtualbox vagrant git-core -y 
```

## Downloading the Docova Project to a Local folder

Open up a terminal and perform the following git command in order to save the Project to a local folder:

```shell
git clone https://github.com/prominic/Docova-Vagrant.git

```
### Configuring the Environment
Once you have navigated into the projects directory. You will need to modify the Hosts.yml to your specific Environment.
Please set the configuration file with the correct, Network and Memory and CPU settings your host machine will allow, as these may vary from system to system, I cannot predict your Machines CPU and Network Requirements. You will need to make sure that you do not over allocate CPU, and RAM. In regards to Networking, you MUST change the networking, you will need to set the IP to that of one that is not in use by any other machine on your network.

If you want to change to a different branch for different Application Builds, change the branch variable to that of an existing branch in this repo, in the Hosts.yml

```
cd Docova-Vagrant
vi Hosts.yml
```
![GitHub Logo](/conf/wiki/images/hosts.yml.png)

#### Commonly Changed Parameters:

* ip: Use any IP on your Internal Network that is NOT in use by any other machine.
* gateway: This is the IP of your Router
* identifier: This is the Hostname of the VM, make sure this is a Fully Qualified Domain Name
* mac: This is your machines Network unique identifier, if you run more than one instance on a network, randonmize this. [Mac Generator](https://www.miniwebtool.com/mac-address-generator/)
* netmask: Set this to the subnet you have your network configured to. This is normally: 255.255.255.0
* name: The Vagrant unique identifier
* cpu: The number of cores you are allocating to this machine. Please beware and do not over allocate. Overallocation may cause instability
* memory: The amount of Memory you are allocating to the machine.  Please beware and do not over allocate. Overallocation may cause instability


Once you have configured the Hosts.yml file. You should now be set to go on getting the VM up and running.

### Starting the VM
The installation process is estimated to take about 15 - 30 Minutes. 

```
vagrant up
```

#### Example of a Succesful run:

<details><summary>Details:</summary>
<p>

#### Example of a Succesful run:

```powershell
 vagrant up
==> vagrant: A new version of Vagrant is available: 2.2.7 (installed version: 2.2.4)!
==> vagrant: To upgrade visit: https://www.vagrantup.com/downloads.html

Bringing machine 'acme_docova' up with 'virtualbox' provider...
==> acme_docova: Box 'Makr44/Docova-Ubuntu-18.04' could not be found. Attempting to find and install...
    acme_docova: Box Provider: virtualbox
    acme_docova: Box Version: >= 0
==> acme_docova: Loading metadata for box 'Makr44/Docova-Ubuntu-18.04'
    acme_docova: URL: https://vagrantcloud.com/Makr44/Docova-Ubuntu-18.04
==> acme_docova: Adding box 'Makr44/Docova-Ubuntu-18.04' (v1) for provider: virtualbox
    acme_docova: Downloading: https://vagrantcloud.com/Makr44/boxes/Docova-Ubuntu-18.04/versions/1/providers/virtualbox.box
    acme_docova: Download redirected to host: vagrantcloud-files-production.s3.amazonaws.com
==> acme_docova: Successfully added box 'Makr44/Docova-Ubuntu-18.04' (v1) for 'virtualbox'!
==> acme_docova: Importing base box 'Makr44/Docova-Ubuntu-18.04'...
==> acme_docova: Matching MAC address for NAT networking...
==> acme_docova: Checking if box 'Makr44/Docova-Ubuntu-18.04' version '1' is up to date...
==> acme_docova: Setting the name of the VM: acme.docova.m4kr.net
==> acme_docova: Pruning invalid NFS exports. Administrator privileges will be required...
==> acme_docova: Clearing any previously set network interfaces...
==> acme_docova: Specific bridge '1) Bridge' not found. You may be asked to specify
==> acme_docova: which network to bridge to.
==> acme_docova: Available bridged network interfaces:
1) viifbr0
2) enp7s0f0
3) enp7s0f1
4) enp8s0f0
5) enp8s0f1
6) enp2s0
7) enp4s0
==> acme_docova: When choosing an interface, it is usually the one that is
==> acme_docova: being used to connect to the internet.
    acme_docova: Which interface should the network bridge to? 7
==> acme_docova: Preparing network interfaces based on configuration...
    acme_docova: Adapter 1: nat
    acme_docova: Adapter 2: bridged
==> acme_docova: Forwarding ports...
    acme_docova: 22 (guest) => 2222 (host) (adapter 1)
==> acme_docova: Running 'pre-boot' VM customizations...
==> acme_docova: Booting VM...
==> acme_docova: Waiting for machine to boot. This may take a few minutes...
    acme_docova: SSH address: 127.0.0.1:2222
    acme_docova: SSH username: vagrant
    acme_docova: SSH auth method: private key
    acme_docova:
    acme_docova: Vagrant insecure key detected. Vagrant will automatically replace
    acme_docova: this with a newly generated keypair for better security.
    acme_docova:
    acme_docova: Inserting generated public key within guest...
    acme_docova: Removing insecure key from the guest if it's present...
    acme_docova: Key inserted! Disconnecting and reconnecting using new SSH key...
==> acme_docova: Machine booted and ready!
[acme_docova] GuestAdditions 6.0.8 running --- OK.
==> acme_docova: Checking for guest additions in VM...
==> acme_docova: Setting hostname...
==> acme_docova: Configuring and enabling network interfaces...
==> acme_docova: Mounting shared folders...
    acme_docova: /vagrant => /root/Docova-Vagrant/conf
==> acme_docova: Running provisioner: shell...
    acme_docova: Running: /tmp/vagrant-shell20200216-18728-ku2h87.sh
    acme_docova: A Branch is not specified, Skipping addition of branch
==> acme_docova: Running provisioner: shell...
    acme_docova: Running: /tmp/vagrant-shell20200216-18728-wkvm23.sh
    acme_docova: alias ..='cd ..'
    acme_docova: alias ...='cd ../..'
    acme_docova: alias h='cd ~'
    acme_docova: alias c='clear'
    acme_docova: alias ll='ls -la'
    acme_docova: Reading package lists...
    acme_docova: Building dependency tree...
    acme_docova:
    acme_docova: Reading state information...
    acme_docova: The following packages were automatically installed and are no longer required:
    acme_docova:   apache2 apache2-bin apache2-data apache2-utils dbconfig-common
    acme_docova:   dbconfig-mysql javascript-common libapr1 libaprutil1 libaprutil1-dbd-sqlite3
    acme_docova:   libaprutil1-ldap libjs-jquery libjs-sphinxdoc libjs-underscore liblua5.2-0
    acme_docova:   libsodium23
    acme_docova: Use 'sudo apt autoremove' to remove them.
    acme_docova: Suggested packages:
    acme_docova:   python-apt-dbg python-apt-doc
    acme_docova: The following NEW packages will be installed:
    acme_docova:   python-apt
    acme_docova: 0 upgraded, 1 newly installed, 0 to remove and 10 not upgraded.
    acme_docova: Need to get 151 kB of archives.
    acme_docova: After this operation, 693 kB of additional disk space will be used.
    acme_docova: Get:1 http://us.archive.ubuntu.com/ubuntu bionic-updates/main amd64 python-apt amd64 1.6.5ubuntu0.2 [151 kB]
    acme_docova: dpkg-preconfigure: unable to re-open stdin: No such file or directory
    acme_docova: Fetched 151 kB in 0s (974 kB/s)
    acme_docova: Selecting previously unselected package python-apt.
    acme_docova: (Reading database ...
(Reading database ... 10% database ... 5%
(Reading database ... 45% database ... 15%
(Reading database ... 55% database ... 50%
    acme_docova: (Reading database ... 60%
    acme_docova: (Reading database ... 65%
    acme_docova: (Reading database ... 70%
    acme_docova: (Reading database ... 75%
    acme_docova: (Reading database ... 80%
    acme_docova: (Reading database ... 85%
    acme_docova: (Reading database ... 90%
    acme_docova: (Reading database ... 95%
(Reading database ... 97214 files and directories currently installed.)
    acme_docova: Preparing to unpack .../python-apt_1.6.5ubuntu0.2_amd64.deb ...
    acme_docova: Unpacking python-apt (1.6.5ubuntu0.2) ...
    acme_docova: Setting up python-apt (1.6.5ubuntu0.2) ...
==> acme_docova: Running provisioner: ansible_local...
    acme_docova: Running ansible-playbook...

PLAY [all] *********************************************************************

TASK [Gathering Facts] *********************************************************
ok: [acme_docova]

TASK [Ensuring Aptitude is installed.] *****************************************
ok: [acme_docova]

TASK [debug] *******************************************************************
ok: [acme_docova] => {
    "msg": "run_letsencrypt is set to: False"
}

TASK [nginx : Update nginx confs for Docova + PHP] *****************************
changed: [acme_docova]

TASK [nginx : Enable site] *****************************************************
changed: [acme_docova]

TASK [mysql : Create mysql user] ***********************************************
ok: [acme_docova]

TASK [mysql : Create mysql database] *******************************************
changed: [acme_docova]

TASK [mysql : Create mysql database] *******************************************
changed: [acme_docova]

TASK [www-data : Update Docova config file] ************************************
ok: [acme_docova] => (item={u'regexp': u'database_driver:', u'line': u'    database_driver: pdo_mysql'})
ok: [acme_docova] => (item={u'regexp': u'database_port:', u'line': u'    database_port: 3306'})
ok: [acme_docova] => (item={u'regexp': u'database_name:', u'line': u'    database_name: docova_db'})
ok: [acme_docova] => (item={u'regexp': u'database_user:', u'line': u'    database_user: docova_db_user'})
ok: [acme_docova] => (item={u'regexp': u'database_password:', u'line': u'    database_password: password12'})
ok: [acme_docova] => (item={u'regexp': u'document_root:', u'line': u'    document_root: /var/docova/attachments'})

TASK [www-data : Running setUpDOCOVA] ******************************************
changed: [acme_docova]

TASK [www-data : Output of setUpDOCOVA] ****************************************
ok: [acme_docova] => {
    "msg": "--------------------------------------------------------------\nSetup DOCOVA SE\n--------------------------------------------------------------\nWARNING: This process will recreate your DOCOVA SE database\nif it already exists. Only use this option for\nbrand new installations.\nTemporarily override entity data types for table creation.\nentity data type conversion complete\n\nCreating docova_db ...\ndocova_db created\n\nCreating schema ...\nSchema creation complete\n\nRemoving override on entity data types.\nentity data type conversion complete\n\nLoading datafixtures ...\nCompleted loading datafixture\n\nInstalling assets\nAssets installation complete\n\nClearing prod cache\nclear cache completed\n\nClearing dev cache\nclear cache completed\n\n-------------------------------------------------------------"
}

TASK [letsencrypt : Upgrade System] ********************************************
skipping: [acme_docova]

TASK [letsencrypt : Add certbot repository] ************************************
skipping: [acme_docova]

TASK [letsencrypt : Install Certbot's Nginx package] ***************************
skipping: [acme_docova]

TASK [letsencrypt : Check if certificate already exists.] **********************
skipping: [acme_docova] => (item={u'servername': u'acme.docova.m4kr.net', u'documentroot': u'/var/html/www/docova/web'})

TASK [letsencrypt : Stop services to allow certbot to generate a cert.] ********
skipping: [acme_docova] => (item=nginx)

TASK [letsencrypt : Generate new Certificate request] **************************
skipping: [acme_docova] => (item={'skip_reason': u'Conditional result was False', 'item': {u'servername': u'acme.docova.m4kr.net', u'documentroot': u'/var/html/www/docova/web'}, 'skipped': True, 'ansible_loop_var': u'item', 'changed': False})

TASK [letsencrypt : Start services after cert has been generated.] *************
skipping: [acme_docova] => (item=nginx)

TASK [letsencrypt : Enabling SSL in Nginx] *************************************
skipping: [acme_docova] => (item={u'regexp': u'ssl_certificate  /etc/letsencrypt/live/acme.docova.m4kr.net/fullchain.pem;', u'line': u'    #ssl_certificate'})
skipping: [acme_docova] => (item={u'regexp': u'ssl_certificate_key /etc/letsencrypt/live/acme.docova.m4kr.net/privkey.pem;', u'line': u'    #ssl_certificate_key'})
skipping: [acme_docova] => (item={u'regexp': u'ssl_protocols TLSv1 TLSv1.1 TLSv1.2;', u'line': u'    #ssl_protocols'})
skipping: [acme_docova] => (item={u'regexp': u'ssl_ciphers HIGH:!aNULL:!MD5;', u'line': u'    #ssl_ciphers'})

RUNNING HANDLER [letsencrypt : restart nginx] **********************************
skipping: [acme_docova]

PLAY RECAP *********************************************************************
acme_docova                : ok=11   changed=5    unreachable=0    failed=0    skipped=9    rescued=0    ignored=0
```
</p>
</details>

## Rebuilding the Project

There are times that the the project may be misconfigured by a typo or wrong value in the Hosts.yml or due to networking issues. As a result of this the VM may not be setup correctly. 

Vagrant commands are highly dependent on the path that your run the commands in. When you run *vagrant up*, you must be inside of the Project folder. If you need to restart the VM, you can do so by running *vagrant reload* however, for this to work, you must be inside of the Vagrant Project folder.


| Common vagrant commands | Modifiers and Options | Default Action                                                  | With Option                                                   |
|-------------------------|-----------------------|-----------------------------------------------------------------|---------------------------------------------------------------|
| vagrant up              | --provision           | Boots the VM, First run Provisions, Subsequent runs simply boot | If the VM has already been created, will run the provisioners |
| vagrant reload          | --provision           | Restarts the VM without Provisioning                            | Restarts the VM runs the provisioners                         |
| vagrant destroy         | -f                    | Vagrant Asks to Destroy VM                                      | Vagrant Destroys the VM                                       |
| vagrant global-status   | --prune               | Lists all VMs and their project paths                           | Lists all VM and their project paths and removes corrupt VMs  |
| vagrant halt            |                       | Shuts down the VM                                               |                                                               |
## Roadmap

See the [open issues](https://github.com/prominic/Docova-Vagrant/issues) for a list of proposed features (and known issues).

## Built With
* [Vagrant](https://www.vagrantup.com/) - Portable Development Environment Suite.
* [VirtualBox](https://www.virtualbox.org/wiki/Downloads) - Hypervisor.
* [Ansible](https://www.ansible.com/) - Virtual Manchine Automation Management.
* [vagrant-vbguest](https://github.com/dotless-de/vagrant-vbguest) - A Vagrant plugin to keep your VirtualBox Guest Additions up to date.
* [vagrant-reload](https://github.com/aidanns/vagrant-reload) - A Vagrant plugin that allows you to reload a Vagrant plugin as a provisioning step.
* [vagrant-disksize](https://github.com/sprotheroe/vagrant-disksize) - A Vagrant plugin to resize disks in VirtualBox.

## Contributing

Please read [CONTRIBUTING.md](https://www.prominic.net) for details on our code of conduct, and the process for submitting pull requests to us.

## Authors

* **Mark Gilbert** - *Initial work* - [Makr91](https://github.com/Makr91)

See also the list of [contributors](https://github.com/prominic/Docova-Vagrant/graphs/contributors) who participated in this project.

## License

This project is licensed under the SSLP v3 License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone whose code was used
