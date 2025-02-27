FROM debian:12-slim as builder
RUN apt-get update && apt-get install -y gettext-base

FROM prom/prometheus:latest
COPY --from=builder /usr/bin/envsubst /usr/bin/envsubst