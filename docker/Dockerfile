FROM ruby:3.1.3-alpine3.17

COPY  usr /usr

ENV BUNDLE_HOME=/usr/local/bundle
ENV BUNDLE_APP_CONFIG=/usr/local/bundle
ENV BUNDLE_DISABLE_PLATFORM_WARNINGS=true
ENV BUNDLE_BIN=/usr/local/bundle/bin
ENV GEM_BIN=/usr/gem/bin
ENV GEM_HOME=/usr/gem
ENV RUBYOPT=-W0

ENV JEKYLL_VAR_DIR=/var/jekyll
ENV JEKYLL_DOCKER_TAG=4.2.2
ENV JEKYLL_VERSION=4.2.2
ENV JEKYLL_DOCKER_COMMIT=fb892998d444b7b2e4074adeb032197f67853c0a
ENV JEKYLL_DOCKER_NAME=jekyll
ENV JEKYLL_DATA_DIR=/srv/jekyll
ENV JEKYLL_BIN=/usr/jekyll/bin
ENV JEKYLL_ENV=development

ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US:en
ENV TZ=America/Chicago
ENV PATH="$JEKYLL_BIN:$PATH"
ENV LC_ALL=en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US

env VERBOSE=false
env FORCE_POLLING=false
env DRAFTS=false

RUN apk --no-cache add \
  zlib-dev \
  libffi-dev \
  build-base \
  libxml2-dev \
  imagemagick-dev \
  readline-dev \
  libxslt-dev \
  libffi-dev \
  yaml-dev \
  zlib-dev \
  vips-dev \
  vips-tools \
  sqlite-dev \
  cmake

RUN apk --no-cache add \
  linux-headers \
  openjdk8-jre \
  less \
  zlib \
  libxml2 \
  readline \
  libxslt \
  libffi \
  git \
  nodejs \
  tzdata \
  shadow \
  bash \
  su-exec \
  npm \
  libressl \
  yarn

RUN echo "gem: --no-ri --no-rdoc" > ~/.gemrc
RUN unset GEM_HOME && unset GEM_BIN && \
  yes | gem update --system

RUN unset GEM_HOME && unset GEM_BIN && yes | gem install --force bundler
RUN gem install jekyll -v4.2.2 \
    -- \
    --use-system-libraries

RUN gem install \
    html-proofer \
    jekyll-reload \
    jekyll-mentions \
    jekyll-coffeescript \
    jekyll-sass-converter \
    jekyll-commonmark \
    jekyll-paginate \
    jekyll-compose \
    jekyll-assets \
    RedCloth \
    kramdown \
    jemoji \
    jekyll-redirect-from \
    jekyll-sitemap \
    jekyll-feed \
    minima \
    -- \
    --use-system-libraries

RUN addgroup -Sg 1000 jekyll
RUN adduser  -Su 1000 -G \
  jekyll jekyll

RUN mkdir -p $JEKYLL_VAR_DIR
RUN mkdir -p $JEKYLL_DATA_DIR
RUN chown -R jekyll:jekyll $JEKYLL_DATA_DIR
RUN chown -R jekyll:jekyll $JEKYLL_VAR_DIR
RUN chown -R jekyll:jekyll $BUNDLE_HOME
RUN rm -rf /home/jekyll/.gem
RUN rm -rf $BUNDLE_HOME/cache
RUN rm -rf $GEM_HOME/cache
RUN rm -rf /root/.gem

RUN mkdir -p /usr/gem/cache/bundle
RUN chown -R jekyll:jekyll \
  /usr/gem/cache/bundle

CMD ["jekyll", "--help"]
ENTRYPOINT ["/usr/jekyll/bin/entrypoint"]
WORKDIR /srv/jekyll
VOLUME  /srv/jekyll
EXPOSE 35729
EXPOSE 4000