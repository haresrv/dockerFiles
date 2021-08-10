FROM ruby:2-stretch

ENV ANT_VERSION=1.10.1
ENV ANT_HOME=/opt/installs/ant

# Installation
RUN cd /tmp \
    && curl http://archive.apache.org/dist/ant/binaries/apache-ant-${ANT_VERSION}-bin.tar.gz > apache-ant-${ANT_VERSION}-bin.tar.gz \
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
RUN mkdir -p /opt/jenkins
RUN cp /tmp/antcontrib.jar /opt/installs/apache-ant-1.10.1/lib/ant-contrib.jar
RUN cp /tmp/sonarqube-ant-task-2.7.1.1951.jar /opt/jenkins/sonarqube-ant-task-2.7.1.1951.jar
ENV LANG C.UTF-8

RUN groupadd --gid 1000 node \
  && useradd --uid 1000 --gid node --shell /bin/bash --create-home node

RUN NODE_VERSION="10.16.0" \
  && ARCH= && dpkgArch="$(dpkg --print-architecture)" \
  && case "${dpkgArch##*-}" in \
    amd64) ARCH='x64';; \
    ppc64el) ARCH='ppc64le';; \
    s390x) ARCH='s390x';; \
    arm64) ARCH='arm64';; \
    armhf) ARCH='armv7l';; \
    i386) ARCH='x86';; \
    *) echo "unsupported architecture"; exit 1 ;; \
  esac \
  && curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-$ARCH.tar.xz" \
  && tar -xJf "node-v$NODE_VERSION-linux-$ARCH.tar.xz" -C /usr/local --strip-components=1 --no-same-owner \
  && rm "node-v$NODE_VERSION-linux-$ARCH.tar.xz"\
  && ln -s /usr/local/bin/node /usr/local/bin/nodejs
  

RUN apt-get update
RUN apt-get install -y -qq openjdk-8-jre openjdk-8-jdk rsync openssh-client python-pip
RUN pip install ast
RUN npm install --silent -g grunt-cli @angular/cli@9.1.12 node-gyp
RUN gem install sass
RUN rm -rf /var/lib/apt/lists/*