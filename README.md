# docker_python

## Setup
* Install [docker-compose](https://docs.docker.com/compose/install/)
* Clone repo by one of the following ways
    * `git clone https://github.com/pythoninthegrass/docker_python.git`
    * Open in GitHub Desktop

## Usage
* Start web server
    ```bash
    cd docker_python/
    docker-compose up --build --remove-orphans
    ```
* Open boilerplate Django server at http://127.0.0.1:8000/
* Ctrl-C to stop server
  * **Note**
    * Running `docker-compose up` will clean up after itself when run without the `-d` switch
    * Analogous to `docker run -it --rm docker_python bash`

## Troubleshooting
* Verify server is listening on port 8000
    ```bash
    $ netstat -na | grep 8000
    tcp46      0      0  *.8000                 *.*                    LISTEN
    ```
* Watch logs in real-time: `docker logs -tf --tail="50" python-docker`
* Check exit code
    ```bash
    $ docker-compose ps
    Name                          Command               State    Ports
    ------------------------------------------------------------------------------
    docker_python_dockerpython_1   python manage.py runserver ...   Exit 0
    ```

## Build
* Remove `docker` volume
    ```bash
    $ docker ps -a
    CONTAINER ID   IMAGE                         COMMAND                  CREATED         STATUS                       PORTS     NAMES
    66696bb035bc   docker_python                 "python manage.py ru…"   8 minutes ago   Exited (0) 36 seconds ago              docker_python_dockerpython_1
    $ docker rm -v 66696bb035bc
    ```
* Remove `docker` image
    ```bash
    docker images
    docker rmi docker_python:latest
    ```
* Rebuild outside of `docker-compose`
    ```bash
    # build
    docker build --tag docker_python .

    # tag as version other than latest
    docker tag <457e6d6c2d25> docker_python:v1.5
    ```

## TODO
* ~~Add GitHub URL~~
* Convert `pip` to `pipenv`
