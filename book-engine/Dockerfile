FROM docker.io/python:3.12-slim

# Install basic tools needed for TeX Live + Pandoc
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        xz-utils \
        fontconfig \
        perl \
        && apt-get clean && rm -rf /var/lib/apt/lists/*

# Install Pandoc (official binary)
RUN curl -L https://github.com/jgm/pandoc/releases/download/3.1.11/pandoc-3.1.11-linux-amd64.tar.gz \
    | tar xz --strip-components 1 -C /usr/local

# Install TeX Live minimal + tlmgr
RUN curl -L https://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz \
    | tar xz && \
    install-tl-*/install-tl \
        --scheme=small \
        --no-interaction && \
    rm -rf install-tl-*

# FIX: Add TeX Live binaries to PATH
ENV PATH="/usr/local/texlive/2026/bin/x86_64-linux:${PATH}"

# Install only the LaTeX packages you need
RUN tlmgr install setspace graphics titlesec geometry fontspec

# Install MinIO client
RUN curl -sSL https://dl.min.io/client/mc/release/linux-amd64/mc \
    -o /usr/local/bin/mc && chmod +x /usr/local/bin/mc

# Install Python dependencies
COPY requirements.txt /tmp/requirements.txt
RUN pip install -r /tmp/requirements.txt

# Copy book engine
COPY engine /engine
WORKDIR /engine
