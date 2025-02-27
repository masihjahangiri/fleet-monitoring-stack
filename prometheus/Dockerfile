FROM debian:12-slim as builder
RUN apt-get update && apt-get install -y gettext-base


FROM prom/prometheus:latest
USER root
COPY --from=builder /usr/bin/envsubst /usr/local/bin/envsubst
RUN chmod +x /usr/local/bin/envsubst

USER       nobody