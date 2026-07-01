FROM docker.io/texlive/texlive:latest

# Install Pandoc (official binary)
RUN curl -L https://github.com/jgm/pandoc/releases/download/3.1.11/pandoc-3.1.11-linux-amd64.tar.gz \
    | tar xz --strip-components 1 -C /usr/local

# Install prebuilt Python (no compiler needed)
RUN curl -L https://github.com/indygreg/python-build-standalone/releases/download/20240524/cpython-3.12.3+20240524-x86_64-unknown-linux-gnu-install_only.tar.gz \
    | tar xz -C /usr/local

# Ensure python3 and pip3 are available
RUN ln -s /usr/local/python/bin/python3 /usr/local/bin/python3 && \
    ln -s /usr/local/python/bin/pip3 /usr/local/bin/pip3

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
