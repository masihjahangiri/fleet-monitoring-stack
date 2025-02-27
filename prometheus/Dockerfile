FROM debian:12-slim as builder
# Install gettext-base which contains envsubst
RUN apt-get update && apt-get install -y gettext-base
# Create a statically linked version of envsubst for BusyBox compatibility
RUN mkdir -p /build/lib
COPY --from=busybox:latest /bin/busybox /build/
RUN ldd /usr/bin/envsubst | grep "=> /" | awk '{print $3}' | xargs -I '{}' cp -v '{}' /build/lib/

FROM prom/prometheus:latest
USER root
# Copy the envsubst binary and its necessary libraries
COPY --from=builder /usr/bin/envsubst /bin/envsubst
COPY --from=builder /build/lib/* /lib/
# Make envsubst executable
RUN chmod +x /bin/envsubst
# Switch back to the non-root user that Prometheus uses
USER nobody