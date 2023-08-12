# What to I learned from this project

- use of different env docker file
  Dockerfile.dev ( run dev server )
  Dockerfile ( run production build )

- how to watch code changes without rebuilding every time
  use of docker volume: reference folder outside of container

- simplify previous work using docker-compose

  - how to docker-comppose find dockerfile.dev ?

- setup test

- nginx setup for production environment

  - multi-step build phases

- use of travis ci

in order to run .dev container
$ docker build -f Dockerfile.dev -t myreactapp .

duplicate dependency issue ( make sure u don't copy node_module from dir to image because it will be installed when creating the image)

run the app
$ docker run -p 3000:3000 myreactapp

=====

# add volumes

$ docker run -p 3000:3000 -v /reactapp/node_modules -v $(pwd):/reactapp myreactapp
where reactapp is workdir in dockerfile

dir:/containerWorkDir
mapping container workdir to directory on left side ( in our example is working directory)

-v /reactapp/node_modules
this prevent mapping node_module file and use container node_module that will be generated with npm install

======

method 1
$ docker exec -t {container-id} npm run test

method 2
add test service to docker-compose

==========

production (check Dockerfile)

$ docker build -t ngx .

<!-- 80 is the default port of nginx -->

$ docker run -p 8888:80 ngx
