### Requirements

- Install docker

## Repos
Git submodules
```bash
git submodule init
git submodule update --remote
```

# Docker CLI summary examples

```bash
$docker-compose up --build
$docker-compose ps
$docker-compose config
$docker-compose restart example_api
$docker inspect example-api
$docker ps
$docker logs $ID
$docker attach $ID
$docker exec -it $ID bash
```

# Start services
At the top path should be the docker-compose.yaml file before to execute docker-compose
```bash
$docker-compose up --build
```

Verify container state
```bash
$docker-compose ps
             Name                            Command               State            Ports
--------------------------------------------------------------------------------------------------
example-api                 example-api/entrypo ...   Up      0.0.0.0:8085->8085/tcp
example-database                       docker-entrypoint.sh postgres    Up      5432/tcp
pgadmin4                           /entrypoint.sh                   Up      443/tcp, 0.0.0.0:80->80/tcp
```
Verify networks
```bash
$docker inspect example-api -f "{{json .NetworkSettings.Networks }}"
{"docker-compose-example":{"IPAMConfig":null,"Links":null,"Aliases":["api","7b122661329a"],"NetworkID":"c01512ab32b5b72103387c437773092043de4589bc6402a960728e03fed4e9b6","EndpointID":"","Gateway":"","IPAddress":"","IPPrefixLen":0,"IPv6Gateway":"","GlobalIPv6Address":"","GlobalIPv6PrefixLen":0,"MacAddress":"","DriverOpts":null}}
```

Test API URL
```bash
$curl http://localhost:8080/health
{"status":"success","data":null,"message":"ok","code":"OK"}
```

4) Need a new `binding.pry` restart the container
```bash
$docker-compose restart example_api
```

# Login to container
```bash
$docker exec -it $ID bash
```

# Tests
In order to get the docker configs you need to login into the container and then run your tests as always
```bash
rake test --trace
```


# pgAdmin

Open your browser and visit http://localhost:80, then type the email and password and add the databases you want to connect, get the address from the env file

