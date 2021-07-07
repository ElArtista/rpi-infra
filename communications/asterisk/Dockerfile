#
### Base image for build stage
#
FROM christoofar/asterisk as build-stage

### Variables to be replaced in configuration
ARG HOST

### Download AGI scripts
RUN set -ex \
 && wget https://raw.githubusercontent.com/zaf/asterisk-googletts/master/googletts.agi -P /scripts \
 && chmod a+x /scripts/googletts.agi

### Copy config folder
COPY ./config /config

### Replace placeholders
RUN set -ex \
 && sed -i "s|{HOST}|${HOST}|g" /config/sip.conf

#
### Base image for production stage
#
FROM christoofar/asterisk as production-stage

### Install prerequisites
RUN set -ex \
 && apt update && apt install -y sox mpg123 perl libwww-perl liblwp-protocol-https-perl

### Copy downloaded scripts from build stage
COPY --from=build-stage /scripts /var/lib/asterisk/agi-bin/

### Copy preprocessed files from build stage
COPY --from=build-stage /config /etc/asterisk/
