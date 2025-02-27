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
COPY --from=builder /lib/ld-musl-*.so.1 /lib/

# Verify installation
RUN envsubst --version

# Maintain original security context
USER nobody