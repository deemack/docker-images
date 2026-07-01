FROM docker.io/pandoc/latex:latest

# Install Python + pip + dependencies
RUN apk update && \
    apk add --no-cache python3 py3-pip bash && \
    rm -rf /var/cache/apk/*

# Install Python dependencies
COPY requirements.txt /tmp/requirements.txt
RUN pip3 install --break-system-packages -r /tmp/requirements.txt
