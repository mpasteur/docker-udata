# uData all-in-one Docker image

This Docker image provide uData as well as all known plugins and themes.

It is packaged to run within uwsgi with gevent support.

By default, it expose the frontend on the port 7000 and expect the following services:

* **MongoDB** on `mongodb:27017`
* **Elasticsearch** on `elasticsearch:9200`
* **Redis** on `redis:6379`

and use the following paths:

* `/udata/udata.cfg` for udata configuration
* `/udata/fs` for storage root (as a volume by default)
* `/udata/public` for public assets root
* `/udata/uwsgi/*.ini` for uwsgi configuration files

You can customize configuration by providing a custom `udata.cfg` or custom uwsgi `ini` file.

A [sample docker-compose.yml file](https://github.com/opendatateam/docker-udata/blob/master/docker-compose.yml)
is also available in the repository.

## Running docker image service

Fetch the latest Docker image version

```bash
docker pull udata/udata
```

Then you can run the container with different configurations:

* a custom udata configuration mounted (here a local `udata.cfg`):

    ```bash
    docker run -v /absolute/path/to/udata.cfg:/udata/udata.cfg udata/udata
    ```

* with custom uwsgi configurations (here contained in the `uwsgi` directory):

    ```bash
    docker run -v `pwd`/uwsgi:/udata/uwsgi udata/udata
    ```

* with file storage as local volume binding:

    ```bash
    docker run -v /path/to/storage:/udata/fs udata/udata
    ```

## Running udata commands

You can also execute `udata` commands with:

```bash
docker run [DOCKER OPTIONS] udata/udata [UDATA COMMAND]
```

By example, to initialise the database with fixtures and initialize the search index:

```bash
docker run -it --rm udata/udata init
```

List all commands with:

```bash
docker run -it --rm udata/udata --help
```

**Note:** Some commands requires either MongoDB, Redis or Elasticsearch to be up and ready.

## Running bash

For debugging purpose you can acces a bash prompt with:

```bash
docker run [DOCKER OPTIONS] udata/udata bash
```
