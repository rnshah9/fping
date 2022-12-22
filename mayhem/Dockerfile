FROM --platform=linux/amd64 ubuntu:22.04 as builder

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y automake pkg-config libtool build-essential clang

COPY . /repo
WORKDIR /repo
RUN ./autogen.sh
RUN ./configure
RUN make -j8

RUN rm -rf /var/lib/apt/lists/*

FROM --platform=linux/amd64 ubuntu:22.04 as package

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y build-essential

COPY --from=builder /repo/src/fping /repo/src/fping