FROM golang:alpine as builder

ENV HUB_VERSION=2.2.9

RUN apk add --no-cache \
      bash \
      curl \
    && curl -sSL -o /tmp/hub-${HUB_VERSION}.tar.gz https://github.com/github/hub/archive/v${HUB_VERSION}.tar.gz \
    && tar -xzf /tmp/hub-${HUB_VERSION}.tar.gz -C /tmp \
    && cd /tmp/hub-${HUB_VERSION} \
    && ./script/build \
    && cp ./bin/hub /root

FROM alpine

COPY --from=builder /root/hub /usr/local/bin

RUN apk add --no-cache \
      git \
      openssh

ENTRYPOINT ["hub"]
