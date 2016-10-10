FROM mono:latest

RUN apt-get update -qq \
&& apt-get install -y wget unzip

# make the default directories 
RUN mkdir -p /Services /Services/Appleseed.Search/ /Services/Appleseed.Search/Index.Service/

# make other directories until paths are fixed in code 
RUN mkdir -p /Services/Appleseed.Search/Data /Services/Appleseed.Search/Data/Public 

# download the config from the git releases / latest , unzip, copy to the destination directory 
RUN cd /tmp \
&& wget https://github.com/Appleseed/search/releases/download/latest/IndexService.zip \
&& unzip IndexService.zip \
&& cd Release \
&& cp -rf * /Services/Appleseed.Search/Index.Service/ \
&& cd /tmp \
&& rm -f IndexService.zip \
&& rm -rf Release

#copy the config from the search-stack to the docker
COPY ./engine.config /Services/Appleseed.Search/Index.Service/Appleseed.Services.Search.Console.exe.config

#copy the wait for it command to be used by compose if needed 
COPY ./wait-for-it.sh /tmp/wait-for-it.sh

WORKDIR /Services/Appleseed.Search/Index.Service/

CMD [ "mono",  "./Appleseed.Services.Search.Console.exe" ]
