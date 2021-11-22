FROM rust:1.56

ARG VERSION=v0.2.15
ARG SHASUM=e5d03a9aa3b9fac7e490391bbe22d4f42c840d31ef9eaf127a03101930cbb7ca

RUN set -eux; \
    apt-get update \
    && apt-get install -y lld curl \
    && rm -rf /var/lib/apt/lists/*
RUN curl -L "https://github.com/mozilla/sccache/releases/download/${VERSION}/sccache-${VERSION}-x86_64-unknown-linux-musl.tar.gz" > sccache.tar.gz \
    && echo "$SHASUM  sccache.tar.gz" \
    && sha256sum sccache.tar.gz \
    && echo "$SHASUM  sccache.tar.gz" | sha256sum -c - \
    && tar xf sccache.tar.gz \
    && mv sccache-$VERSION-x86_64-unknown-linux-musl/sccache /usr/local/bin/sccache \
    && chmod +x /usr/local/bin/sccache \
    && rm -r sccache.tar.gz sccache-$VERSION-x86_64-unknown-linux-musl
ENV JUST_VERSION=0.10.4
RUN set -eux; \
    curl --fail --location "https://github.com/casey/just/releases/download/${JUST_VERSION}/just-${JUST_VERSION}-x86_64-unknown-linux-musl.tar.gz" --output /tmp/just.tar.gz; \
    tar --directory "/usr/local/bin" -xzvf "/tmp/just.tar.gz" --wildcards "just"; \
    rm /tmp/just.tar.gz; \
    chmod +x /usr/local/bin/just; \
    just --version
ENV CARGO_UDEPS_VERSION=v0.1.24
RUN set -eux; \
    curl --fail --location "https://github.com/est31/cargo-udeps/releases/download/${CARGO_UDEPS_VERSION}/cargo-udeps-${CARGO_UDEPS_VERSION}-x86_64-unknown-linux-gnu.tar.gz" --output /tmp/cargo-udeps.tar.gz; \
    tar --directory "/usr/local/bin" -xzvf "/tmp/cargo-udeps.tar.gz" --strip-components 2 --wildcards "*/cargo-udeps"; \
    rm /tmp/cargo-udeps.tar.gz; \
    chmod +x /usr/local/bin/cargo-udeps; \
    cargo-udeps --version