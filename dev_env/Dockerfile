# from here: https://github.com/AGhost-7/docker-dev/blob/master/tutorial/readme.md
# and here: https://medium.com/@nielssj/docker-volumes-and-file-system-permissions-772c1aee23ca
FROM ubuntu:bionic

# This tutorial does not include how to optimize the image size, therefore
# we won't be placing various commands on a single line.
RUN apt-get update

# Install sudo command...
RUN apt-get install -y sudo

# Feel free to change this to whatever your want
ENV DOCKER_USER gautam

# make the user group
RUN addgroup --gid 1222 dockgroup

# Start by creating our passwordless user.
RUN adduser \
  --disabled-password \
  --gecos "" \
  # --force-badname \
  --ingroup dockgroup \
  "$DOCKER_USER"

# Give root priviledges
RUN adduser "$DOCKER_USER" sudo

# Give passwordless sudo. This is only acceptable as it is a private
# development environment not exposed to the outside world. Do NOT do this on
# your host machine or otherwise.
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Set the user to be our newly created user by default.
USER "$DOCKER_USER"

# This will determine where we will start when we enter the container.
WORKDIR "/dockvol"

# The sudo message is annoying, so skip it
# RUN touch ~/.sudo_as_admin_successful

# We will need this to build c/c++ dependencies. This is common enough
# in all my various projects that I include it in my base image; there are
# often transitive dependencies in Python/NodeJs/Rust projects which require
# c/c++ compilation.
RUN sudo apt-get install -y build-essential

# The Ubuntu image does not include curl. I prefer it, but it isn't necessary.
# Note that if you decide to not install this you will need to use wget instead
# for some of the installation commands in this tutorial.
RUN sudo apt-get install -y curl

# We will need git so we can clone repositories
RUN sudo apt-get install -y git

# SSH is not bundled by default. I always use ssh to push to Github.
RUN sudo apt-get install -y openssh-client

# The manuals are always handy for development.
RUN sudo apt-get install -y man-db

# Get basic tab completion
RUN sudo apt-get install -y bash-completion


# tmux
RUN sudo apt-get install -y tmux

# python
# RUN sudo apt-get install -y python3.8

# pip
RUN sudo apt install -y python3-venv python3-pip

# jupyter lab
RUN pip3 install jupyter
RUN pip3 install jupyterlab

# add to path
ENV PATH="~/.local/bin:${PATH}"

# expose a port that jupyter lab can use
EXPOSE 8888

# django
RUN pip3 install django

# expose a port for django
EXPOSE 8000

# neovim
RUN sudo apt install neovim -y

# jekyll, from https://jekyllrb.com/docs/installation/ubuntu/
# and https://bundler.io/v2.0/guides/bundler_docker_guide.html
RUN sudo apt-get install -y ruby-full zlib1g-dev 

ENV GEM_HOME="/usr/local/bundle"
ENV PATH="$GEM_HOME/bin:$GEM_HOME/gems/bin:$PATH"

RUN sudo gem install jekyll bundler
COPY Gemfile .
COPY Gemfile.lock .
RUN bundle install

# pre-commit
RUN pip3 install pre-commit

# link python and pip to python3 and pip3
RUN sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 0
RUN sudo update-alternatives --install /usr/bin/pip pip /usr/bin/pip3 0

# pandas
RUN pip install pandas
