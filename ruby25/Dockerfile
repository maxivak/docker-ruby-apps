FROM phusion/passenger-ruby25:1.0.1


#
ENV TERM xterm
#RUN export TERM=xterm


# base packages
RUN apt-get update --fix-missing
RUN apt-get install -y  --no-install-recommends wget iputils-ping rsync





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
# node v8 (LTS)
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs



# yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && \
    apt-get install -y --no-install-recommends yarn


# libs
RUN apt-get update && \
    apt-get install -y --no-install-recommends imagemagick

# mysql
RUN apt-get install -y --no-install-recommends mysql-client libmysqlclient-dev


# apps
USER app

RUN mkdir -p /home/app/apps

# nginx apps
#RUN rm /etc/nginx/sites-enabled/default

#COPY files/sites/ /etc/nginx/sites-enabled/



# Clean up APT when done.
USER root
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

