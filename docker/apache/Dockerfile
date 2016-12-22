#++++++++++++++++++++++++++++++++++++++
# HTTPD Docker container
#++++++++++++++++++++++++++++++++++++++
#
# Official images:
#
#   httpd - Apache Webserver
#           https://hub.docker.com/_/httpd/
#
#++++++++++++++++++++++++++++++++++++++

FROM httpd:2.4

MAINTAINER Rahul Singh <rahul.singh@anant.us>

RUN apt-get update -qq \
&& apt-get install -y wget unzip 

# listen on 8080 so that it can be used in the same network as nginx for proxy
RUN sed -i 's/Listen\ 80/Listen\ 8080/g' /usr/local/apache2/conf/httpd.conf

# make the default directories 
RUN mkdir -p /Services /Services/Appleseed.Search/ /Services/Appleseed.Search/Web.User
RUN mkdir -p /usr/local/apache2/htdocs/solr/ /usr/local/apache2/htdocs/elastic/

# download the dist from the git releases / latest , unzip, copy to the destination directory 
RUN mkdir -p /tmp 
RUN cd /tmp \
&& wget https://github.com/Appleseed/search-web-user/archive/latest.zip \
&& unzip latest.zip \
&& cd search-web-user-latest \
&& cp -rf Appleseed.Search.Web.User.Ng.Solr/* /usr/local/apache2/htdocs/solr/ \
&& cp -rf Appleseed.Search.Web.User.Ng.Elastic/* /usr/local/apache2/htdocs/elastic/ \
&& cd /tmp \
&& rm -f latest.zip \
&& rm -rf search-web-user-latest

EXPOSE 8080
