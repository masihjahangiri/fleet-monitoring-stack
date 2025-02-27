# Stage 1: Build compatible envsubst with libraries
FROM alpine:latest as builder
RUN apk add --no-cache gettext

# Stage 2: Target Prometheus image
FROM prom/prometheus:latest

# Create necessary directories and set permissions
USER root
RUN mkdir -p /usr/lib

# Copy binary and required libraries
COPY --from=builder /usr/bin/envsubst /usr/bin/
COPY --from=builder /usr/lib/libintl.so.8 /usr/lib/
# COPY --from=builder /lib/ld-musl-x86_64.so.1 /lib/

# Verify binary functionality
RUN envsubst --version

# Maintain original security context
USER nobody