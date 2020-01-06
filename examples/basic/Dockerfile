FROM node:lts-stretch

ENV HOME=/home/node
ENV NPM_CONFIG_PREFIX=$HOME/.npm-global

# Limit the number of unecessary erros
ARG DEBIAN_FRONTEND=noninteractive

# Install Additional dependecies
RUN \
  apt-get update && \
  apt-get install --yes \
  --no-install-recommends \
  build-essential \
  libcairo2-dev \
  libjpeg-dev \
  libjpeg-turbo-progs \
  libpango1.0-dev \
  libgif7 \
  libgif-dev \
  g++ \
  nasm \
  ffmpeg \
  libavcodec-extra57 \
  wget

USER node

# Create npm-global and testcafe dir as user before setting WORKDIR.
# This prevents premissions errors with npm ci/install as non-root user.
RUN mkdir $NPM_CONFIG_PREFIX \
  && mkdir -p $HOME/testcafe/node_modules

# Set the working directory to /usr/src/testcafe after creationing it.
WORKDIR $HOME/testcafe

# Copy package files into container at /usr/src/testcafe
COPY --chown=node:node package*.json $HOME/testcafe/

# Install any needed packages specified in package.json
RUN npm ci

ENTRYPOINT ["/bin/bash", "-c"]

