# Lightweight base with glibc and shell
FROM debian:stable-slim

# Install only essential build tools (still lightweight)
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        xz-utils \
        fontconfig \
        && apt-get clean && rm -rf /var/lib/apt/lists/*

# Install Pandoc (official binary)
RUN curl -L https://github.com/jgm/pandoc/releases/download/3.1.11/pandoc-3.1.11-linux-amd64.tar.gz \
    | tar xz --strip-components 1 -C /usr/local

# Install TeX Live minimal (tiny footprint)
RUN curl -L https://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz \
    | tar xz && \
    install-tl-*/install-tl \
        --profile=/dev/null \
        --scheme=small \
        --no-interaction && \
    rm -rf install-tl-*

# Install only the LaTeX packages you need
RUN tlmgr install setspace graphics titlesec geometry fontspec

# Install Python manually (small footprint)
RUN curl -L https://www.python.org/ftp/python/3.12.3/Python-3.12.3.tgz \
    | tar xz && \
    cd Python-3.12.3 && \
    ./configure --enable-optimizations && \
    make -j$(nproc) && \
    make install && \
    cd .. && rm -rf Python-3.12.3

# Install MinIO client
RUN curl -sSL https://dl.min.io/client/mc/release/linux-amd64/mc \
    -o /usr/local/bin/mc && chmod +x /usr/local/bin/mc

# Install Python dependencies
COPY requirements.txt /tmp/requirements.txt
RUN pip3 install --break-system-packages -r /tmp/requirements.txt

# Copy book engine
COPY engine /engine
WORKDIR /engine
