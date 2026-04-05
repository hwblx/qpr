# Build:
#   docker build -t qpr-test -f tests/docker/Dockerfile .
#
# Run:
#   docker run -it --rm --privileged qpr-test
#

FROM docker:dind

# Install bash and coreutils (for realpath)
RUN apk add --no-cache bash coreutils

# Ensure docker client talks to the local dind daemon
ENV DOCKER_HOST=unix:///var/run/docker.sock

# Set the working directory
WORKDIR /app

# Copy the script and templates into the image
COPY qpr /usr/local/bin/qpr
RUN chmod +x /usr/local/bin/qpr
COPY templates/ /app/templates/

# Start the Docker daemon in the background and then launch bash
CMD ["sh", "-c", "dockerd-entrypoint.sh > /dev/null 2>&1 & sleep 5; /bin/bash"]
