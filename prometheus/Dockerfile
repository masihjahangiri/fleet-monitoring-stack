# Use Alpine-based builder to ensure compatibility with Prometheus image
FROM alpine:latest as builder
RUN apk add --no-cache gettext

# Use the official Prometheus image (Alpine-based)
FROM prom/prometheus:latest

# Switch to root to perform privileged operations
USER root

# Copy envsubst from the Alpine builder to the Prometheus image
COPY --from=builder /usr/bin/envsubst /usr/bin/envsubst

# Ensure the copied binary is executable
RUN chmod +x /usr/bin/envsubst

# Switch back to the non-root user (maintains security best practices)
USER nobody