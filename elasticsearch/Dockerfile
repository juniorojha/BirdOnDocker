FROM ubuntu:16.04
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update

RUN apt-get install -y --no-install-recommends software-properties-common && add-apt-repository -y ppa:webupd8team/java && \
    apt-get update && \
    (echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections) && \
    apt-get install --no-install-recommends -y oracle-java8-installer && \
    rm -rf /var/cache/oracle-jdk8-installer && \
    echo "networkaddress.cache.ttl=60" >> /usr/lib/jvm/java-8-oracle/jre/lib/security/java.security && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle


RUN groupadd -g 1000 elasticsearch && useradd elasticsearch -u 1000 -g 1000

RUN gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys D27D666CD88E42B4 && \
    gpg --export --armor D27D666CD88E42B4 | apt-key add -

RUN gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys A278B781FE4B2BDA && \
    gpg --export --armor A278B781FE4B2BDA | apt-key add -
# && \
    #add-apt-repository -y "deb http://packages.elastic.co/elasticsearch/5.x/debian stable main" --keyserver hkp://keyserver.ubuntu.com:80  && \
    #apt-get update && \
    #apt-get install -y --no-install-recommends elasticsearch=5.4.0
# RUN apt-get install -y wget
RUN wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.4.0.deb
RUN apt install ./elasticsearch-5.4.0.deb
RUN apt-get update

WORKDIR /usr/share/elasticsearch

RUN set -ex && for path in data logs config config/scripts; do \
        mkdir -p "$path"; \
        chown -R elasticsearch:elasticsearch "$path"; \
    done

COPY logging.yml /usr/share/elasticsearch/config/
COPY elasticsearch.yml /usr/share/elasticsearch/config/

USER elasticsearch

ENV PATH=$PATH:/usr/share/elasticsearch/bin

CMD ["elasticsearch"]

EXPOSE 9200 9300


