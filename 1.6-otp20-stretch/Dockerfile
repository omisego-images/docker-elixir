FROM omisegoimages/erlang:20-stretch
MAINTAINER Kridsada Thanabulpong <sirn@omise.co>

ENV ELIXIR_VERSION="v1.6.4"

RUN set -xe && \
    ELIXIR_DOWNLOAD_URL="https://github.com/elixir-lang/elixir/archive/${ELIXIR_VERSION}.tar.gz" && \
    ELIXIR_DOWNLOAD_SHA256="c12a4931a5383a8a9e9eb006566af698e617b57a1f645a6cb132a321b671292d" && \
    build_deps="build-essential" && \
    apt-get update && \
    apt-get install -y --no-install-recommends $build_deps && \
    curl -fsL -o elixir-src.tar.gz "${ELIXIR_DOWNLOAD_URL}" && \
    echo "${ELIXIR_DOWNLOAD_SHA256}  elixir-src.tar.gz" |sha256sum -c - && \
    mkdir -p /usr/local/src/elixir && \
    tar -xzC /usr/local/src/elixir --strip-components=1 -f elixir-src.tar.gz && \
    rm elixir-src.tar.gz && \
    cd /usr/local/src/elixir && \
    make -j$(nproc) && \
    make install && \
    apt-get purge -y --auto-remove $build_deps && \
    apt-get clean && \
    rm -rf /usr/local/src/elixir

CMD ["iex"]