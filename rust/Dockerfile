FROM rust:1.56

ARG VERSION=v0.2.15
ARG SHASUM=e5d03a9aa3b9fac7e490391bbe22d4f42c840d31ef9eaf127a03101930cbb7ca

RUN apt-get update \
    && apt-get install -y lld curl \
    && rm -rf /var/lib/apt/lists/* \
    &&  curl -L "https://github.com/mozilla/sccache/releases/download/${VERSION}/sccache-${VERSION}-x86_64-unknown-linux-musl.tar.gz" > sccache.tar.gz \
    && echo "$SHASUM  sccache.tar.gz" \
    && sha256sum sccache.tar.gz \
    && echo "$SHASUM  sccache.tar.gz" | sha256sum -c - \
    && tar xf sccache.tar.gz \
    && mv sccache-$VERSION-x86_64-unknown-linux-musl/sccache /usr/local/bin/sccache \
    && chmod +x /usr/local/bin/sccache \
    && rm -r sccache.tar.gz sccache-$VERSION-x86_64-unknown-linux-musl && cargo install -f just