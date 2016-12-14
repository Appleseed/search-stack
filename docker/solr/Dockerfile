#++++++++++++++++++++++++++++++++++++++
# SolR Docker container
#++++++++++++++++++++++++++++++++++++++
#
# Official images:
#
#   solr - official solr
#                   https://hub.docker.com/_/solr/
# 
#++++++++++++++++++++++++++++++++++++++
# TODO : use newer solr containers (5/6) 
# TODO : find out a way to have persistent storage from host , 
# etc, maybe with storage volumes that load from host
#++++++++++++++++++++++++++++++++++++++

FROM makuk66/docker-solr:4.10.4 
MAINTAINER Rahul Singh <rahul.singh@anant.us>

RUN mkdir -p /opt/solr/example/solr/appleseed-public/
RUN mkdir -p /opt/solr/example/solr/appleseed-public/data
COPY ./anant/appleseed-search/solr/ /opt/solr/example/solr/
