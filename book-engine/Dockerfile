FROM docker.io/pandoc/core:latest

# Install Python, pip, bash, curl
RUN apt-get update && \
    apt-get install -y python3 python3-pip bash curl && \
    apt-get clean

# Install MinIO client
RUN curl -sSL https://dl.min.io/client/mc/release/linux-amd64/mc \
    -o /usr/local/bin/mc && \
    chmod +x /usr/local/bin/mc

# Update TeX Live and install required packages
RUN tlmgr update --self && \
    tlmgr install setspace graphics titlesec geometry fontspec

COPY requirements.txt /tmp/requirements.txt
RUN pip3 install --break-system-packages -r /tmp/requirements.txt
