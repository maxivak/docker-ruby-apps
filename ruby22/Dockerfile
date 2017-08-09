FROM phusion/passenger-ruby23:0.9.20


#
ENV TERM xterm
#RUN export TERM=xterm


# base packages
RUN apt-get update
RUN apt-get -y install iputils-ping


# setpwd
#RUN echo 'root:pass' | chpasswd
#RUN echo 'app:pass' | chpasswd


# ssh
RUN rm -f /etc/service/sshd/down

ADD files/sshd_config /etc/ssh/sshd_config

RUN chown root:root /var/run/sshd && chmod 700 /var/run/sshd


# nginx
RUN rm -f /etc/service/nginx/down


# apps
RUN mkdir -p /home/app/apps

# nginx apps
#RUN rm /etc/nginx/sites-enabled/default

#COPY files/sites/ /etc/nginx/sites-enabled/

# debug
#RUN touch /home/app/myapp/public/1.html
#RUN echo "hello" > /home/app/myapp/public/1.html
