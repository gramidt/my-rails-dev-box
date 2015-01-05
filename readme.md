# A Virtual Machine to Jump Start Your Ruby on Rails Development

## What's in this magical box?

Ruby / Rails
* RVM
* Ruby 2.0.0 & 2.1.0
* Bundler

Source Control
* Git

Databases
* SQLite
* MySQL
* PostgreSQL (9.1)
* MongoDB

Caching
* Redis (2.6.5)

Misc.
* Qt
* MailCatcher

## What are the requirements to get up and running?

* [VirtualBox] (https://www.virtualbox.org)

* [Vagrant 1.1+] (http://vagrantup.com)

## So the prerequisites are installed, how do I get started?

    host $ git clone https://github.com/granvilleschmidt/my-rails-dev-box.git
    host $ cd my-rails-dev-box
    host $ vagrant up

BOOM! Everything is now ready for development. Magic right?

Note: It may take upwards of a few minutes the first time you
run 'vagrant up', since it will need to download the base box.

After the installation has finished, you can access the magical box with

    host $ vagrant ssh
    Welcome to Ubuntu 12.04 LTS (GNU/Linux 3.2.0-23-generic x86_64)
    ...
    vagrant@my-rails-dev-box:/vagrant/projects$

Given that port 3000 is the default port for new Rails apps, we went ahead and forwarded that port to the magical box, so you can access your web applications from your host machine.

NOTICE: If you are using Rails 4.2 and greater, you need to use _rails s -b 0.0.0.0_ to start the server, as the Rails 4.2 changed the listening address default from 0.0.0.0 to localhost. 

## This seems like voodoo. How do you expect me to work on a magical box from my host machine?

Well it turns out that Vagrant mounts the my-rails-dev-box directory as _/vagrant_ within the magical box. So with a little additional black  magic (aka. one liner bash script), you can
just start working directly out of the current directory which happens to be _/vagrant/projects_ after running _vagrant ssh_.

## Additional Notes

MailCatcher

Add the following to your 'environment/development.rb', and MailCatcher will catch any
outgoing mail.

    config.action_mailer.delivery_method = :smtp
    config.action_mailer.smtp_settings = { :address => "localhost", :port => 1025 }

Then all you have to do is run _mailcatcher --ip=0.0.0.0_, and you can access the application at  _http://localhost:1080_.

PostgreSQL

    # login
    sudo -u postgres psql postgres

    # create user
    sudo -u postgres createuser -s <username>

    # set password
    ALTER USER <username> WITH PASSWORD ‘<newpassword>’;
