FROM alpine:latest as builder
RUN apk add --no-cache gettext

FROM prom/prometheus:latest
COPY --from=builder /usr/bin/envsubst /usr/local/bin/envsubst