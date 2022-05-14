# Devbox-packer

## Pre-requisites

The following is required to follow along

[Packer](https://www.packer.io/downloads) (Tested on Packer v1.8.0)

After downloading Packer, unzip the package. Packer runs as a single binary named packer.

Finally, make sure that the packer binary is available on your PATH. This process will differ depending on your operating system.

- Mac or Linux

  Print a colon-separated list of locations in your PATH.

  ```
  $ echo $PATH
  ```

  Move the Packer binary to one of the listed locations. This command assumes that the binary is currently in your downloads folder and that your PATH includes /usr/local/bin, but you can customize it if your locations are different.

  ```
  $ mv ~/Downloads/packer /usr/local/bin/
  ```

- Windows

  Add the directory which has Packer installed to the PATH variables.

# Building

Run packer build after creating the template for Packer:

```
$ packer build file_name.json
```

```
$ packer build file_name.pkr.hcl
```

The above command will create a directory named output-vagrant where you can find a package.box file and a Vagrantfile.

You need the package.box file for configuring your virtual environment with Vagrant.

# Configuring Vagrant

After creating the custom Vagrant box, you have to configure the virtual environment with Vagrant.

## Create a Vagrantfile:

```
$ vagrant init dev-env
```

Where dev-env is the value assigned to the config.vm.box variable in the Vagrantfile. You can replace it according to your needs.

Add the package.box file to Vagrant:

```
$ vagrant box add dev-env output-vagrant/package.box
```

Now your virtual environment is ready. You can initialize it and log in through SSH.

```
$ vagrant up
$ vagrant ssh
```

You're ready to go!

## To convert json file to hcl

```
packer hcl2_upgrade -output-file=file_name.pkr.hcl file_name.pkr.json
```
