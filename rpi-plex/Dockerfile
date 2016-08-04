FROM resin/rpi-raspbian:jessie
MAINTAINER Richard Hopkins-Lutz

# Dependencies
RUN wget -O - https://dev2day.de/pms/dev2day-pms.gpg.key | apt-key add - \
 && echo "deb [arch=armhf] https://dev2day.de/pms/ jessie main" >> /etc/apt/sources.list.d/pms.list  \
 && apt-get update -y \
 && apt-get upgrade -y \
 && apt-get install locales wget ca-certificates apt-transport-https mkvtoolnix libexpat1 libc6 -y 

# Setup locales
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/g' /etc/locale.gen \
 && locale-gen

# Setup volumes
#  - /config holds the server settings
#  - /data is where media should be mounted
VOLUME ["/config", "/data"]

# Plex config environment vars
ENV HOME=/config

# Plex server port
EXPOSE 32400

ENV TERM=xterm

# Grab RPI Plex package
RUN apt-get install plexmediaserver-installer:armhf -y 

ADD start.sh /start.sh
RUN chmod +x start.sh

CMD ["bash", "start.sh"]
