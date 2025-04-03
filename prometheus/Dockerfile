FROM --platform=$BUILDPLATFORM alpine:latest as builder
RUN apk add --no-cache gettext curl

ARG TARGETARCH
RUN GOMPLATE_ARCH=$TARGETARCH && \
    case "$GOMPLATE_ARCH" in \
      amd64) GOMPLATE_ARCH=amd64 ;; \
      arm64) GOMPLATE_ARCH=arm64 ;; \
    esac && \
    curl -sSL "https://github.com/hairyhenderson/gomplate/releases/latest/download/gomplate_linux-$GOMPLATE_ARCH" -o /usr/bin/gomplate && \
    chmod +x /usr/bin/gomplate && \
    gomplate --version

FROM prom/prometheus:latest

USER root

RUN mkdir -p /usr/lib /lib

COPY --from=builder /usr/bin/envsubst /usr/bin/
COPY --from=builder /usr/bin/gomplate /usr/bin/
COPY --from=builder /usr/lib/libintl.so.8 /usr/lib/
COPY --from=builder /lib/ld-musl-*.so.1 /lib/

RUN envsubst --version && gomplate --version

USER nobody