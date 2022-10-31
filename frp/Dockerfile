FROM golang:1.19-bullseye as build

ARG FRP_VERSION=0.45.0
ARG BUILD_TARGET=frpc

WORKDIR /build

RUN set -ex; \
    \
    apt update && apt install unzip; \
    \
    curl -SsL https://github.com/fatedier/frp/archive/refs/tags/v${FRP_VERSION}.zip -o ./frp.zip; \
    unzip frp.zip; \
    cd frp-${FRP_VERSION}; \
    go build -o /build/${BUILD_TARGET} cmd/${BUILD_TARGET}/main.go;

FROM debian:bullseye

COPY --from=build /build/${BUILD_TARGET} /usr/local/bin

CMD [ "${BUILD_TARGET}" ]