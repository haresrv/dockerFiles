FROM openjdk:8-alpine3.9

#####
# Ant
#####

# Preparation
ENV ANT_VERSION 1.10.1
ENV ANT_HOME /opt/installs/apache-ant-${ANT_VERSION}

# Installation
RUN cd /tmp \
    && wget -O apache-ant-${ANT_VERSION}-bin.tar.gz http://archive.apache.org/dist/ant/binaries/apache-ant-${ANT_VERSION}-bin.tar.gz \
    && mkdir -p ${ANT_HOME} \
    && tar -zxf apache-ant-${ANT_VERSION}-bin.tar.gz \
    && mv apache-ant-${ANT_VERSION}/* ${ANT_HOME}/ \
    && rm apache-ant-${ANT_VERSION}-bin.tar.gz \
    && rm -rf apache-ant-${ANT_VERSION} \
    && rm -rf ${ANT_HOME}/manual

ENV PATH ${PATH}:${ANT_HOME}/bin

# Ant Contrib to lib
COPY . /tmp
RUN mkdir -p /opt/installs/apache-ant-1.10.1/lib/
RUN cp /tmp/antcontrib.jar /opt/installs/apache-ant-1.10.1/lib/ant-contrib.jar

#NODE
ENV ALPINE_MIRROR "http://dl-cdn.alpinelinux.org/alpine"
RUN echo "${ALPINE_MIRROR}/v3.9/main/" >> /etc/apk/repositories
RUN apk add -U --no-cache nghttp2-dev nodejs npm
RUN apk add ruby --repository=http://dl-cdn.alpinelinux.org/alpine/v3.11/main
RUN apk add rsync openssh-client
RUN npm install -g grunt-cli
RUN rm -rf /tmp/* /var/cache/apk/*