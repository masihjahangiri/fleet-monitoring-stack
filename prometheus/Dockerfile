# Stage 1: Build compatible components
FROM --platform=$BUILDPLATFORM alpine:latest as builder
RUN apk add --no-cache gettext

# Stage 2: Target Prometheus image
FROM prom/prometheus:latest

USER root

# Install minimum libc components
RUN mkdir -p /usr/lib /lib

# Copy envsubst and required libraries
COPY --from=builder /usr/bin/envsubst /usr/bin/
COPY --from=builder /usr/lib/libintl.so.8 /usr/lib/
# Use a more reliable way to copy the musl library
COPY --from=builder /lib/ld-musl-*.so.1 /lib/

# Verify installation
RUN envsubst --version

# Create directories for Prometheus configuration
RUN mkdir -p /etc/prometheus/rules

# Copy Prometheus configuration files
# Note: The actual files will be mounted as volumes from docker-compose

# Set proper permissions
RUN chown -R nobody:nobody /etc/prometheus /prometheus

USER nobody

# The entrypoint is defined in docker-compose.yml to allow for template substitution