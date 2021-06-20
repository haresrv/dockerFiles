FROM starefossen/ruby-node:latest

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
RUN cp /tmp/antcontrib.jar /opt/installs/apache-ant-1.10.1/lib/ant-contrib.jar

RUN apt-get update
RUN apt-get install -y -qq openjdk-8-jre openjdk-8-jdk rsync openssh-client python-pip
RUN pip install ast
RUN npm install -g grunt-cli
RUN gem install sass
RUN rm -rf /var/lib/apt/lists/*