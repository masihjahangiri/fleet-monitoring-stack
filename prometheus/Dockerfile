FROM debian:12-slim as builder
RUN apt-get update && apt-get install -y gettext-base

FROM prom/prometheus:latest
USER root
# Copy the binary to multiple locations to ensure it's found
COPY --from=builder /usr/bin/envsubst /bin/envsubst
COPY --from=builder /usr/bin/envsubst /usr/bin/envsubst
COPY --from=builder /usr/bin/envsubst /usr/local/bin/envsubst

# Make all copies executable
RUN chmod +x /bin/envsubst /usr/bin/envsubst /usr/local/bin/envsubst

# Switch back to the non-root user that Prometheus uses
USER nobody