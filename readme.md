# Docker image for Ruby applications

* based on https://github.com/phusion/passenger-docker

* Nginx, Passenger, SSH server



# Build

* build from github

* build with Ruby 2.3

```
docker build -t my-apps github.com/maxivak/docker-ruby-apps.git/ruby23
```


# Run

* place nginx server configs in folder '/path/to/nginx/sites'

* place code for apps in folder '/path/to/apps'


* run container

```
docker run -d --name my-apps \
-p 8080:80 \
-v /path/to/nginx/sites:/etc/nginx/sites-enabled/ \
-v /path/to/apps:/home/app/apps \
-v /path/to/nginx/logs:/var/log/nginx/  \
my-apps /sbin/my_init 
```


* example of nginx server config:

```
# /etc/nginx/sites-enabled/myapp.conf:
server {
    listen 80;
    server_name myapp.local;
    root /home/app/apps/myapp/current/public;

    # The following deploys your Ruby/Python/Node.js/Meteor app on Passenger.

    # Not familiar with Passenger, and used (G)Unicorn/Thin/Puma/pure Node before?
    # Yes, this is all you need to deploy on Passenger! All the reverse proxying,
    # socket setup, process management, etc are all taken care automatically for
    # you! Learn more at https://www.phusionpassenger.com/.
    passenger_enabled on;
    passenger_user app;

    # If this is a Ruby app, specify a Ruby version:
    #passenger_ruby /usr/bin/ruby2.3;

    passenger_app_env production;
}


```