### What is it?

A Vagrant configuration that starts up a PostgreSQL database in a virtual machine. This was original forked from https://github.com/jackdb/pg-app-dev-vm and modified for the purpose of creating a postgreSQL test environment. It includes the Pagila sample database that was cloned from https://github.com/devrimgunduz/pagila.git

### Installation

First install [Vagrant] and [Virtual Box].

Then, run the following to create a new PostgreSQL pagila database virtual machine:

    
    # Clone it locally:
    $ git clone https://github.com/berkanyiildirim/postgresql-pagila-vm.git pg-pagila

    # Enter the cloned directory:
    $ cd pg-pagila

    # Delete the old .git and README:
    $ rm -rf README.md .git LICENSE
    
    # Optionally edit the database username/password and PostgreSQL version (default 13):
    $ $EDITOR Vagrant-setup/bootstrap.sh

### Usage

    # Start up the virtual machine:
    $ vagrant up

    # Stop the virtual machine:
    $ vagrant halt

### What does it do?

It creates a virtual server running Centos7 with the latest version of PostgreSQL (*as of writing 13*) installed. It setup Pagila database and edits the PostgreSQL configuration files to allow network access. 

Once it has started up it will print out how to access the database on the virtual machine. It will look something like this:

    $ vagrant up
    Bringing machine 'default' up with 'virtualbox' provider...
    [... truncated ...]
    Your PostgreSQL database has been setup and can be accessed on your local machine on the forwarded port (default: 15432)
      Host: localhost
      Port: 15432
      Database: pagila
      Username: pagila
      Password: dbpass

    Admin access to postgres user via VM:
      vagrant ssh
      sudo su - postgres

    psql access to pagila database user via VM:
      vagrant ssh
      sudo su - postgres
      PGUSER=pagila PGPASSWORD=dbpass psql -h localhost pagila

    Env variable for application development:
      DATABASE_URL=postgresql://pagila:dbpass@localhost:15432/pagila

    Local command to access the database via psql:
      PGUSER=pagila PGPASSWORD=dbpass psql -h localhost -p 15432 pagila

### Why use the shell provisioner?

Or alternatively, why not [Chef](http://www.getchef.com/chef/), [Puppet](http://puppetlabs.com/), [Ansible](http://www.ansibleworks.com/), or [Salt](http://www.saltstack.com/)?

Mainly because it's simple and anybody with a basic knowledge of shell scripting can tweak the `bootstrap.sh` to their liking.

### License

This is released under the MIT license. See the file [LICENSE](LICENSE).

[Virtual Box]: https://www.virtualbox.org/
[Vagrant]: http://www.vagrantup.com/
