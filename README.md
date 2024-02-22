# Laravel custom docker

Custom docker starter package for Laravel

## Installation

1. Clone this repository into a desired directory `git@github.com:bakicdj/laravel-docker-starter.git docker`
2. Make sure your project directory is in the same level as this one
3. Copy `docker-compose.yml.sample` from `docker` directory to root as `docker-compose-yml`
4. In `docker-compose.yml` file find and replace `appname` in all places with your project name
5. Run `docker compose up -d`

### Project root dir should look like this:
``` 
project_name
    app                 -> your laravel project
    docker              -> dir where you cloned it
    docker-compose.yml  -> the one you copied from docker dir
```

## Usage

`docker compose exec php zsh`
