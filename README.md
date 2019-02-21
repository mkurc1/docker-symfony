# Docker Symfony 4 (PHP7.2-FPM - NGINX - MySQL)

Simple docker configuration for Symfony 4 applications. This stack run with docker and docker-compose (1.7 or higher).

## Configure

1. Create a `.env` from the `.env.dist` file and update it into your configurations.

## License

The bundle is released under the [MIT License](LICENSE).

## Build and run containers

```
$ docker-compose build
$ docker-compose up -d
```

If you use Mac OS you should use this commands:
```
$ docker-compose -f docker-compose.yml -f docker-compose.mac.yml build
$ docker-compose -f docker-compose.yml -f docker-compose.mac.yml up -d
```
It's definitely improve performance on Mac OS.
