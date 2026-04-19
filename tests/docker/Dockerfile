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
RUN apk add --no-cache bash dash zsh busybox-extras coreutils inotify-tools curl checkbashisms shellcheck

# Ensure docker client talks to the local dind daemon
ENV DOCKER_HOST=unix:///var/run/docker.sock

# Set the working directory
WORKDIR /app

# Copy script, test and templates into the image
COPY qpr /usr/local/bin/qpr
RUN chmod +x /usr/local/bin/qpr
RUN cp /usr/local/bin/qpr /app/qpr

COPY tests/test-qpr /usr/local/bin/test-qpr
RUN chmod +x /usr/local/bin/test-qpr
RUN cp /usr/local/bin/test-qpr /app/test-qpr

COPY templates/ /app/templates/

# Start the Docker daemon in the background and then launch a shell
CMD ["sh", "-c", "dockerd-entrypoint.sh > /dev/null 2>&1 & \
echo -n 'Waiting for Docker daemon '; \
until docker info >/dev/null 2>&1; do \
    sleep 1; \
    echo -n '.'; \
done; \
echo ''; \
echo 'Docker daemon (DinD) is up!'; \
/usr/local/bin/test-qpr; \
exec /bin/sh"]
