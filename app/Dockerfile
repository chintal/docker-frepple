FROM ubuntu:18.04
MAINTAINER Chintalagiri Shashank <shashank.chintalagiri@gmail.com>

RUN apt-get update 
RUN apt-get -y install apt-utils
RUN apt-get -y install python3 python3-pip
RUN apt-get -y install apache2-utils
RUN apt-get -y install apache2 --no-install-recommends
RUN apt-get -y install libapache2-mod-wsgi-py3 --no-install-recommends
RUN apt-get -y install libxerces-c3.2
RUN apt-get -y install python3-psycopg2
RUN apt-get -y install curl

RUN apt-get clean 

RUN a2enmod wsgi

RUN ln -s /usr/bin/python3 /usr/bin/python
RUN ln -s /usr/bin/pip3 /usr/bin/pip 

RUN pip install --upgrade pip

COPY requirements.txt /
RUN pip install -r requirements.txt

COPY install.sh /

# Comment these two lines to prevent downloading and extracting the source tarball every time. 
RUN mkdir /debdir
RUN curl -SL https://github.com/frePPLe/frepple/releases/download/6.6.0/frepple_6.6.0_linux_debian.tgz | tar -xvzC /debdir

# Uncomment the following line to just use locally available deb files instead.
#COPY debdir /debdir

RUN chmod +x /install.sh
RUN ./install.sh


COPY --chown=root:frepple djangosettings.py /etc/frepple/djangosettings.py
RUN chmod g+r /etc/frepple/djangosettings.py

RUN a2enmod expires
RUN a2enmod wsgi
RUN a2enmod ssl
RUN a2dissite 000-default.conf
RUN a2ensite frepple.conf

#CMD ["frepplectl", "migrate", "--noinput"]

EXPOSE 80 3500 

CMD ["apache2ctl", "-D", "FOREGROUND"]

