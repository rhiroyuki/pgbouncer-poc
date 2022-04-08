FROM ruby:3.1.1-alpine3.15

RUN apk add --update --no-cache \
  git \
  build-base \
  postgresql-dev \
  tzdata \
  bash

WORKDIR /tmp

COPY Gemfile ./
COPY Gemfile.lock ./
RUN gem update --system && \
      gem install bundler -v $(tail -1 Gemfile.lock | xargs) --conservative --default && \
      bundle install --jobs=$(nproc) --retry=3

WORKDIR /app
ADD . /app

CMD bin/rails server -p ${PORT} -b 0.0.0.0
