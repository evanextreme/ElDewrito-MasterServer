# Set the base image to Ubuntu
FROM    ubuntu

# File Author / Maintainer
MAINTAINER emoose

# Install Node.js and other dependencies
RUN apt-get update && \
    apt-get -y install sudo curl && \
    curl -sL https://deb.nodesource.com/setup_4.x | sudo bash - && \
    apt-get -y install python build-essential nodejs

RUN useradd -m docker && echo "docker:docker" | chpasswd && adduser docker sudo

USER root
CMD /bin/bash

# Install nodemon
RUN sudo npm install -g nodemon

USER docker

# Provides cached layer for node_modules
ADD package.json /tmp/package.json
RUN cd /tmp && npm install
RUN mkdir -p /src && cp -a /tmp/node_modules /src/

# Define working directory
WORKDIR /src
ADD . /src

# Expose port
EXPOSE  8080

# Run app using nodemon
CMD ["nodemon", "/src/index.js"]
