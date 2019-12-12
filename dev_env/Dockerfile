# from here: https://github.com/AGhost-7/docker-dev/blob/master/tutorial/readme.md
FROM ubuntu:bionic

# This tutorial does not include how to optimize the image size, therefore
# we won't be placing various commands on a single line.
RUN apt-get update

# Install sudo command...
RUN apt-get install -y sudo

# Feel free to change this to whatever your want
ENV DOCKER_USER developer

# Start by creating our passwordless user.
RUN adduser --disabled-password --gecos '' "$DOCKER_USER"

# Give root priviledges
RUN adduser "$DOCKER_USER" sudo

# Give passwordless sudo. This is only acceptable as it is a private
# development environment not exposed to the outside world. Do NOT do this on
# your host machine or otherwise.
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Set the user to be our newly created user by default.
USER "$DOCKER_USER"

# This will determine where we will start when we enter the container.
WORKDIR "/home/$DOCKER_USER"

# The sudo message is annoying, so skip it
RUN touch ~/.sudo_as_admin_successful

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
RUN sudo apt-get install python3.8

# pip
sudo apt install python3-venv python3-pip