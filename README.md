# mycompose

Homelab docker compose helper

## Demo

![demo](./assets/demo.gif)

## Features

- Detect automatically where docker-compose.yml are located
- Check Update of running docker-compose images (work on AMD64 and ARM)
- Update docker-compose images with a backup (volume and version of previous latest) locally
- Rollback to previous update with the previous backup
- Start and stop docker-compose
- Edit docker-compose.yml 

## :warning: Requirements

Use: 
```
mycompose compatibility
```

- No `'` or `"` in docker-compose image line
```
image: misterbabou/gptwol:latest
#image: 'misterbabou/gptwol:latest' will not work
```
- All you volumes should be located in a appdata folder for each application for backup before update
tree example:
```
|-- RootDir
|  |-- App1
|  |  |-- docker-compose.yml
|  |  |-- appdata
|        |-- volume1
|        |-- volume2
|  |-- App2
|  |  |-- docker-compose.yml
|  |  |-- appdata
|        |-- volume1
...
```
- Those following command are required : `jq` `curl` `docker` and (`docker-compose` or `compose` plugin for docker cli). For compose the program will prefer compose plugin but will choose docker-compose if not present.

## Deploy

- Download command (Change <version> see https://github.com/Misterbabou/mycompose/releases) : 
```
sudo curl -L https://github.com/Misterbabou/mycompose/releases/download/<version>/mycompose -o /usr/local/bin/mycompose
```

- Make this command executable
```
sudo chmod +x /usr/local/bin/mycompose
```

- Run your first command :

Check all Commands with examples
```
mycompose help
```

List all of your containers
```
mycompose list
```


## Known issue 

- If you have docker-compose version under 2.3.0, `docker compose ls` will not work to find your docker-compose RootDir, either upgrade or use setdir command
- If all of your docker-compose are located in same RootDir but `docker compose ls` can't find absolute Path command will not work. Use setdir command to manualy define Rootdir 
- If you have multiple Rootdir for docker-compose in your system command will not work. Use recommended tree (see Requirements)

