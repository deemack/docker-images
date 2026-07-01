# TeX Live base that Buildah can pull anonymously
FROM docker.io/texlive/texlive:latest

# Install Pandoc (official binary)
RUN curl -L https://github.com/jgm/pandoc/releases/download/3.1.11/pandoc-3.1.11-linux-amd64.tar.gz \
    | tar xz --strip-components 1 -C /usr/local

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

# Install only the LaTeX packages you need
RUN tlmgr install setspace graphics titlesec geometry fontspec

# Install Python dependencies
COPY requirements.txt /tmp/requirements.txt
RUN pip3 install --break-system-packages -r /tmp/requirements.txt

# Copy book engine
COPY engine /engine
WORKDIR /engine
