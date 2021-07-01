### Base image for build stage
FROM christoofar/asterisk as build-stage

### Variables to be replaced in configuration
ARG HOST

### Copy config folder
COPY ./config /config

### Replace placeholders
RUN set -ex \
 && sed -i "s|{HOST}|${HOST}|g" /config/sip.conf

### Base image for production stage
FROM christoofar/asterisk as production-stage

### Copy preprocessed files from build stage
COPY --from=build-stage /config /etc/asterisk/
