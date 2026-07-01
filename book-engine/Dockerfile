FROM docker.io/pandoc/latex:latest

# Install Python + Pip
RUN apt-get update && \
    apt-get install -y python3 python3-pip && \
    apt-get clean

# Install Python dependencies
COPY requirements.txt /tmp/requirements.txt
RUN pip3 install -r /tmp/requirements.txt

# Copy your book engine scripts
COPY engine /engine
WORKDIR /engine
