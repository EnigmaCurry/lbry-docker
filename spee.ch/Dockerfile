FROM ubuntu:18.04 as prep
LABEL MAINTAINER="leopere [at] nixc [dot] us"
RUN apt-get update && \
    apt-get install -y \
      git \
      curl \
      unzip \
      ffmpeg \
      nodejs \
      npm \
      imagemagick
ARG REPO=https://github.com/lbryio/spee.ch
ARG VERSION=master
RUN git clone ${REPO} /spee.ch && \
    cd /spee.ch && \
    git checkout ${VERSION} && \
    rm -rf .git && \
    npm install

FROM ubuntu:18.04 as app
RUN apt-get update && \
    apt-get install -y \
      nodejs \
      ffmpeg \
      imagemagick \
      npm
COPY --from=prep /spee.ch /spee.ch
WORKDIR /spee.ch
CMD /usr/bin/npm run build && /usr/bin/npm run start
