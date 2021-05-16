# Simple Flask App




[![Build Status](https://travis-ci.com/Marta162/se_hello_printer_app.svg?branch=master)](https://travis-ci.com/Marta162/se_hello_printer_app)

[![StatusCake](https://app.statuscake.com/button/index.php?Track=5961411&Days=1&Design=2)]

Aplikacja Dydaktyczna wyświetlająca imię i wiadomość w różnych formatach dla zajęć
o Continuous Integration, Continuous Delivery i Continuous Deployment.

- W projekcie wykorzystamy virtual environment, dla utworzenia hermetycznego środowisko dla aplikacji:

  ```
  # tworzymy hermetyczne środowisko dla bibliotek aplikacji:
  $ python3 -m venv .venv

  # aktywowanie hermetycznego środowiska
  $ source .venv/bin/activate
  $ pip install -r requirements.txt
  $ pip install -r test_requirements.txt

  # zobacz
  $ pip list
  ```

  Sprawdź: [tutorial venv](https://docs.python.org/3/tutorial/venv.html) oraz [biblioteki flask](http://flask.pocoo.org).

- Uruchamianie applikacji:

  ```
  # jako zwykły program
  $ python main.py

  # albo:
  $ PYTHONPATH=. FLASK_APP=hello_world flask run
  ```

- Uruchamianie testów (see: http://doc.pytest.org/en/latest/capture.html):

  # bez makefile
  $ PYTHONPATH=. py.test
  $ PYTHONPATH=. py.test --verbose -s
  ```

- Kontynuując pracę z projektem, aktywowanie hermetycznego środowiska dla aplikacji py:

  ```
  # deaktywacja
  $ deactivate
  ```

  ```
  ...

  # aktywacja
  $ source .venv/bin/activate
  ```

- Integracja z TravisCI:

#dodaj plik .travis.yml :

'''
language: python
python:
    -"3.6"
  install:
    -make deps
  script:
    -make test
'''

  ```
  # miejsce na twoje notatki

  # dodanie deps, init, test i run do projektu, w pliku Makefile
  # wywolanie
  # make deps
  # make init
  # make run
  # make test
  ```

# Pomocnicze

## Ubuntu

- Instalacja dockera: [dockerce howto](https://docs.docker.com/install/linux/docker-ce/ubuntu/)

'''Dockerfile :

FROM python:3
ARG APP_DIR=/usr/src/hello_world_printer
WORKDIR /tmp
ADD requirements.txt /tmp/requirements.txt
RUN pip install -r /tmp/requirements.txt
RUN mkdir -p $APP_DIR
ADD hello_world/ $APP_DIR/hello_world/
ADD main.py $APP_DIR
CMD PYTHONPATH=$PYTHONPATH:/usr/src/hello_world_printer \FLASK_APP=hello_world flask run --host=0.0.0.0
'''

komendy dockera w konsoli :

$ make docker_build
$ docker images# aby zobaczyć zbudowany obraz dockera

dopisz komendy Dockera w makefile:

'''
docker_run: docker_build
    docker run \
      --name hello-world-printer-dev \
        -p 5000:5000 \
        -d hello-world-printer

## Centos

- Instalacja docker-a:

  ```
  $ yum remove docker \
        docker-common \
        container-selinux \
        docker-selinux \
        docker-engine

  $ yum install -y yum-utils

  $ yum-config-manager \
      --add-repo \
      https://download.docker.com/linux/centos/docker-ce.repo

  $ yum makecache fast
  $ yum install -y docker-ce
  $ systemctl start docker
  ```
