FROM docker.io/pandoc/latex:latest

RUN apk update && \
    apk add --no-cache python3 py3-pip bash && \
    rm -rf /var/cache/apk/*

RUN tlmgr update --self && \
    tlmgr install setspace graphics titlesec geometry fontspec

# Install MinIO client
RUN curl -sSL https://dl.min.io/client/mc/release/linux-amd64/mc \
    -o /usr/local/bin/mc && \
    chmod +x /usr/local/bin/mc

COPY requirements.txt /tmp/requirements.txt
RUN pip3 install --break-system-packages -r /tmp/requirements.txt
