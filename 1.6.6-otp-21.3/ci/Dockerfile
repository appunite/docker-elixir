FROM erlang:21.3.1-slim

# elixir expects utf8.
ENV ELIXIR_VERSION="v1.6.6-otp-21" \
  LANG=C.UTF-8

RUN set -xe \
  && ELIXIR_DOWNLOAD_URL="https://repo.hex.pm/builds/elixir/${ELIXIR_VERSION}.zip" \
  && buildDeps=' \
    ca-certificates \
    curl \
    unzip \
  ' \
  && apt-get update \
  && apt-get install -y --no-install-recommends $buildDeps \
  && curl -fSL -o elixir-precompiled.zip $ELIXIR_DOWNLOAD_URL \
  && unzip -d /usr/local elixir-precompiled.zip \
  && rm elixir-precompiled.zip \
  && apt-get purge -y --auto-remove $buildDeps \
  && rm -rf /var/lib/apt/lists/*

CMD ["iex"]

RUN mix local.hex --force
RUN mix local.rebar --force

RUN set -xe \
  && ciDeps=' \
  build-essential \
  ca-certificates \
  git \
  postgresql-client \
  ' \
  && apt-get update \
  && apt-get install -y --no-install-recommends $ciDeps \
  && apt-get purge -y \
  && rm -rf /var/lib/apt/lists/*
