FROM adoptopenjdk:8-jdk-hotspot-bionic

ENV ANT_VERSION=1.8.0
ENV ANT_HOME=/opt/ant

# Download and extract apache ant to opt folder
RUN curl http://archive.apache.org/dist/ant/binaries/apache-ant-1.8.0-bin.tar.gz > apache-ant-1.8.0-bin.tar.gz

RUN tar -zvxf apache-ant-${ANT_VERSION}-bin.tar.gz -C /opt/
RUN ln -s /opt/apache-ant-${ANT_VERSION} /opt/ant
RUN rm -f apache-ant-${ANT_VERSION}-bin.tar.gz

# add executables to path
RUN update-alternatives --install "/usr/bin/ant" "ant" "/opt/ant/bin/ant" 1 
RUN update-alternatives --set "ant" "/opt/ant/bin/ant" 

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get install -qq --no-install-recommends nodejs
RUN npm install -g grunt-cli
RUN rm -rf /var/lib/apt/lists/*
