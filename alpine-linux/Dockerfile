FROM alpine:3.11
RUN apk add openjdk8 python2

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
RUN rm -f /etc/apk/repositories
RUN echo "${ALPINE_MIRROR}/v3.11/main/" >> /etc/apk/repositories
RUN echo "${ALPINE_MIRROR}/v3.11/community/" >> /etc/apk/repositories
RUN apk add nghttp2 nghttp2-dev rsync openssh-client
RUN apk add nodejs-current nodejs-npm ruby ruby-dev build-base libffi-dev
RUN gem install sass
RUN npm install -g grunt-cli