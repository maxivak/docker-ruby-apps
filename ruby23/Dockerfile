FROM phusion/passenger-ruby23:0.9.20


#
ENV TERM xterm
#RUN export TERM=xterm


# base packages
RUN apt-get update --fix-missing
RUN apt-get -y install wget iputils-ping rsync


# setpwd
#RUN echo 'root:pass' | chpasswd
#RUN echo 'app:pass' | chpasswd


# ssh
RUN rm -f /etc/service/sshd/down

ADD files/sshd_config /etc/ssh/sshd_config

RUN chown root:root /var/run/sshd && chmod 700 /var/run/sshd


# nginx
RUN rm -f /etc/service/nginx/down

# nodejs
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get update
RUN apt-get -y install nodejs

# yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update
RUN apt-get -y install yarn




# libs
RUN apt-get update
RUN apt-get -y install imagemagick

# mysql
RUN apt-get -y install mysql-client libmysqlclient-dev


# apps
RUN mkdir -p /home/app/apps

# nginx apps
#RUN rm /etc/nginx/sites-enabled/default

#COPY files/sites/ /etc/nginx/sites-enabled/

# debug
#RUN touch /home/app/myapp/public/1.html
#RUN echo "hello" > /home/app/myapp/public/1.html



# Clean up APT when done.
USER root
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
