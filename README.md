# Vagrant

### Install Virtualbox for vagrant background.
`# brew cask install virtualbox`

### Install Vagrant
`# brew cask install vagrant`

### Run Vagrant
Copy Varantfile into root of your project. Run `vagrant up` or `vagrant up --provision` if you are changed Vagrantfile.
For ssh connection to machine, run `vagrant ssh`.

> For the running docker-compose up automatically run `vagrant plugin install vagrant-docker-compose` and configure Vagrantfile.

> Important! If you want to save the data of your containers in the virtual machine, you need to save it in the `Volumes`.

# DONE!
