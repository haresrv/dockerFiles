FROM frekele/java:jdk8

ENV ANT_VERSION=1.8.0
ENV ANT_HOME=/opt/ant

# change to tmp folder
WORKDIR /tmp

# Download and extract apache ant to opt folder
RUN wget --no-check-certificate --no-cookies http://archive.apache.org/dist/ant/binaries/apache-ant-${ANT_VERSION}-bin.tar.gz

RUN tar -zvxf apache-ant-${ANT_VERSION}-bin.tar.gz -C /opt/
RUN ln -s /opt/apache-ant-${ANT_VERSION} /opt/ant
RUN rm -f apache-ant-${ANT_VERSION}-bin.tar.gz

# add executables to path
RUN update-alternatives --install "/usr/bin/ant" "ant" "/opt/ant/bin/ant" 1 
RUN update-alternatives --set "ant" "/opt/ant/bin/ant" 

# change to root folder
WORKDIR /root