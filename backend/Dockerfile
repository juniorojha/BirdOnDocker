FROM ubuntu:16.04
FROM maven:3.5-jdk-9

ENV sunbird_cassandra_host "http://localhost"
ENV sunbird_cassandra_port "9042"
ENV sunbird_cassandra_username ""
ENV sunbird_cassandra_password ""
ENV sunbird_es_host "http://localhost"
ENV sunbird_es_port "9200"
ENV sunbird_learner_actor_host ""
ENV sunbird_learner_actor_port ""
ENV sunbird_sso_url ""
ENV sunbird_sso_realm ""
ENV sunbird_sso_username ""
ENV sunbird_sso_password ""
ENV sunbird_sso_client_id ""
ENV ekstep_content_search_base_url ""
ENV ekstep_authorization ""
ENV sunbird_installation "IITB_X"
ENV sunbird_quartz_mode "embedded"ls
ENV sunbird_sso_publickey ""

RUN apt-get update
RUN apt-get install -y git-core

#RUN git clone https://github.com/project-sunbird/sunbird-utils.git
#RUN git clone https://github.com/project-sunbird/sunbird-lms-service.git
#RUN git clone https://github.com/project-sunbird/sunbird-lms-mw.git

ADD . /

# RUN git submodule foreach git pull origin master

WORKDIR sunbird-utils/
RUN mvn clean install

WORKDIR sunbird-lms-mw/
RUN mvn clean install

WORKDIR sunbird-lms-service/
RUN mvn clean install
