# dev_env

A general development docker

## creating a persistent local volume
[./vol-setup](./vol-setup)

## build comamnd
[./docker-build](./docker-build)

## run command
[./docker-run](./docker-run)

## running jupyter

```
jupyter lab --ip 0.0.0.0
```

## sources

Base is from here: https://github.com/AGhost-7/docker-dev/blob/master/tutorial/readme.md

### Jupyter lab
https://stackoverflow.com/questions/49024624/how-to-dockerize-jupyter-lab


https://stackoverflow.com/questions/35313876/after-installing-with-pip-jupyter-command-not-found


### persisting data
From https://medium.com/@nielssj/docker-volumes-and-file-system-permissions-772c1aee23ca

### Django

```
pip3 install Django==3.0
```

https://medium.com/zeitcode/a-simple-recipe-for-django-development-in-docker-bonus-testing-with-selenium-6a038ec19ba5

### Jekyll
https://jekyllrb.com/docs/installation/ubuntu/

https://bundler.io/v2.0/guides/bundler_docker_guide.html

https://success.docker.com/article/use-a-script-to-initialize-stateful-container-data

```
bundle exec jekyll serve --host=0.0.0.0
```

## To do
- [x] set up git global info (from file maybe?)
  - updated docker run to add the host gitconfig
- [ ] learn and set up vim
