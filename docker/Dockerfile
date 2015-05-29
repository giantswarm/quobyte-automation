FROM ubuntu:15.04

RUN apt-get update && \
    apt-get install -y software-properties-common && \
    echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
    add-apt-repository -y ppa:webupd8team/java && \
    apt-get update && \
    apt-get install -y oracle-java8-installer && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /var/cache/oracle-jdk8-installer

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

ENV QUOBYTE_REPO_ID _insert_quobyte_repo_id_here_

RUN apt-get update && \
    apt-get install -y \
    apt-transport-https \
    python-software-properties

RUN wget -q https://support.quobyte.com/repo/2/${QUOBYTE_REPO_ID}/xUbuntu_14.10/Release.key -O - | apt-key add - && \
    echo "deb https://support.quobyte.com/repo/2/${QUOBYTE_REPO_ID}/xUbuntu_14.10 ./" > /etc/apt/sources.list.d/quobyte.list

RUN apt-get update && \
    apt-get install -y \
    quobyte-server \
    quobyte-client \
    dnsutils

COPY ./main.sh /opt/main.sh
ENTRYPOINT ["/opt/main.sh"]
