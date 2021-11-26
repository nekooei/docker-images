FROM rust:1.31

RUN apt-get install wget tar
WORKDIR /tmp

RUN wget https://github.com/kartevonmorgen/openfairdb/releases/download/v0.10.5/openfairdb_v0.10.5.x86_64-unknown-linux-musl.tar.xz

RUN mkdir -p /backend
RUN tar xJf openfairdb_v0.10.5.x86_64-unknown-linux-musl.tar.xz -C /backend

WORKDIR /backend
RUN chmod +x ./openfairdb

ENV RUST_LOG info

CMD ["./openfairdb"]