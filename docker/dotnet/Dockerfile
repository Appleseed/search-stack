#++++++++++++++++++++++++++++++++++++++
# dotnet Docker container
#++++++++++++++++++++++++++++++++++++++
#
# Official images:
#
#   dotnet - official dotnet core
#                   https://hub.docker.com/r/microsoft/aspnet/
#
#++++++++++++++++++++++++++++++++++++++

FROM microsoft/aspnet

COPY . /app
WORKDIR /app
RUN ["dnu", "restore"]

EXPOSE 5005
ENTRYPOINT ["dnx", "-p", "project.json", "kestrel"]
