FROM erlang:20.2.2

# elixir expects utf8.
ENV ELIXIR_VERSION="1.6.1" \
	LANG=C.UTF-8

RUN apt update && apt install -y unzip ssh && apt-get clean

RUN set -xe \
	&& ELIXIR_DOWNLOAD_URL="https://github.com/elixir-lang/elixir/archive/v${ELIXIR_VERSION#*@}.zip" \
	&& ELIXIR_DOWNLOAD_SHA256="058bc8a389615132208dafce52a222d0447d307002a24e187ac3c56e9b82c365" \
	&& curl -fSL -o elixir-src.zip $ELIXIR_DOWNLOAD_URL \
	&& echo "$ELIXIR_DOWNLOAD_SHA256 elixir-src.zip" | sha256sum -c - \
	&& mkdir -p /usr/src/elixir-src \
	&& unzip elixir-src.zip -d /usr/src/elixir-src \
	&& rm elixir-src.zip \
	&& cd /usr/src/elixir-src/elixir-${ELIXIR_VERSION} \
	&& make -j$(nproc) \
	&& make install \
	&& rm -rf /usr/src/elixir-src

CMD ["iex"]
