# Build:
#   docker build -t qpr-test -f tests/docker/Dockerfile .
#
# Run:
#   docker run -it --rm --privileged qpr-test
#
# Test with different shells:
#   sh /usr/local/bin/qpr --help
#   bash /usr/local/bin/qpr --help
#   dash /usr/local/bin/qpr --help
#   zsh /usr/local/bin/qpr --help
#

FROM docker:dind

# Install shells and coreutils (for realpath)
RUN apk add --no-cache bash dash zsh busybox-extras coreutils checkbashisms shellcheck

# Ensure docker client talks to the local dind daemon
ENV DOCKER_HOST=unix:///var/run/docker.sock

# Set the working directory
WORKDIR /app

# Copy the script and templates into the image
COPY qpr /usr/local/bin/qpr
RUN chmod +x /usr/local/bin/qpr
RUN cp /usr/local/bin/qpr /app/qpr
COPY templates/ /app/templates/

# Start the Docker daemon in the background and then launch a shell
# CMD ["sh", "-c", "dockerd-entrypoint.sh > /dev/null 2>&1 & sleep 5; /bin/sh"]
CMD ["sh", "-c", "\
    echo 'Starting docker daemon...'; \
    dockerd-entrypoint.sh > /dev/null 2>&1 & \
    sleep 5; \
    echo -n 'Running checkbashisms on qpr... '; checkbashisms /usr/local/bin/qpr && echo 'passed!' || echo 'failed!'; \
    echo -n 'Running shellcheck on qpr... '; shellcheck --shell=sh /usr/local/bin/qpr && echo 'passed!' || echo 'failed!'; \
    exec /bin/sh \
"]
