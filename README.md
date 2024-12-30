# Deploy

## Makefile
**Generally it's better to use "make" commands.**  
Makefile commands streamline process of accesing docker image and executing commands in it.

## Base Docker commands

**Build container**
<pre>
docker-compose -f deploy/docker-compose.yml up --build -d
</pre>

**Stop and remove container**
<pre>
docker-compose -f deploy/docker-compose.yml down
</pre>

**Verify container is set up properly**
<pre>
docker-compose -f deploy/docker-compose.yml ps
</pre>

**Enter dotnet-app container**
<pre>
docker-compose -f deploy/docker-compose.yml exec app bash
</pre>

**Enter Postgres container**
<pre>
docker-compose -f deploy/docker-compose.yml exec db bash
</pre>

## .Net

### First setting up .Net project
appsettings.json contains default settings.
appsettings.Development.json contains settings for develop environment. Copying all configs from appsettings.json not neccesary. Write down only the ones which you want to overwrite.