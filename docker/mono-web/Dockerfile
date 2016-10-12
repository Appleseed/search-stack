FROM mono:latest

MAINTAINER Rahul Singh <rahul.singh@anant.us>

RUN apt-get update -qq \
&& apt-get install -y wget unzip mono-xsp4

# make the default directories 
RUN mkdir -p /Services /Services/Appleseed.Search/ /Services/Appleseed.Search/Web.Admin /Services/Appleseed.Search/Index.Service

# download the dist from the git releases / latest , unzip, copy to the destination directory 
# RUN cd /tmp \
# && wget https://github.com/Appleseed/search/releases/download/latest/IndexService.zip \
# && unzip IndexService.zip \
# && cd Release \
# && cp -rf * /Services/Appleseed.Search/Index.Service/ \
# && cd /tmp \
# && rm -f IndexService.zip \
# && rm -rf Release

# right now copying from local 
COPY ./dist/Appleseed.Search.Web.Admin.zip /tmp/Appleseed.Search.Web.Admin.zip
RUN cd /tmp \
&& unzip Appleseed.Search.Web.Admin.zip \
&& cd Appleseed.Search.Web.Admin \
&& cp -rf * /Services/Appleseed.Search/Web.Admin/ \
&& cd /tmp \
&& rm -f Appleseed.Search.Web.Admin.zip \
&& rm -rf Appleseed.Search.Web.Admin

# rigging for testing only because we'll be mounting it later' in storage
RUN mv /Services/Appleseed.Search/Web.Admin/Appleseed.Search /Services/Appleseed.Search/Index.Service 

#TODO mount this from a local file 
#copy the config from the search-stack to the docker - should really mount from a local file 
COPY ./engine.config /Services/Appleseed.Search/Index.Service/Appleseed.Services.Search.Console.exe.config

#copy the config for the search web admin so that it is pointing to the right place relatively ... 
#may not need this at some point 
COPY ./web.config /Services/Appleseed.Search/Web.Admin/Appleseed.Search.Admin/Web.config

WORKDIR /Services/Appleseed.Search/Web.Admin/Appleseed.Search.Admin/

EXPOSE 9000

ENV MONO_OPTIONS "--debug"

ENTRYPOINT ["xsp4", "--port=9000", "--nonstop", "--debug"]