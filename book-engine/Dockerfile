# Base image: full TeX Live distribution (no Debian required)
FROM texlive/texlive:latest

# Install Pandoc manually (official tarball)
RUN curl -L https://github.com/jgm/pandoc/releases/download/3.1.11/pandoc-3.1.11-linux-amd64.tar.gz \
    | tar xz --strip-components 1 -C /usr/local

# Install Python manually (source build)
RUN curl -L https://www.python.org/ftp/python/3.12.3/Python-3.12.3.tgz \
    | tar xz && \
    cd Python-3.12.3 && \
    ./configure --enable-optimizations && \
    make -j$(nproc) && \
    make install

# Install MinIO client (mc)
RUN curl -sSL https://dl.min.io/client/mc/release/linux-amd64/mc \
    -o /usr/local/bin/mc && \
    chmod +x /usr/local/bin/mc

# Install Python dependencies
COPY requirements.txt /tmp/requirements.txt
RUN pip3 install --break-system-packages -r /tmp/requirements.txt

# Copy book engine
COPY engine /engine
WORKDIR /engine
