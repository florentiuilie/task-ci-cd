FROM python:3.9-slim

# Install necessary system packages
RUN apt-get update && \
    apt-get -y upgrade && \
    DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
    libpq-dev gcc python3-pip && \
    rm -rf /var/lib/apt/lists/*

# Set the working directory
WORKDIR /sample-app

# Copy only necessary files first
COPY requirements.txt requirements-server.txt ./

# Install dependencies
RUN pip3 install -r requirements.txt && pip3 install -r requirements-server.txt

# Copy the application code
COPY . .

# Copy and set up entrypoint script
COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

# Set environment variables
ENV LC_ALL="C.UTF-8"
ENV LANG="C.UTF-8"

# Expose application port
EXPOSE 8000/tcp

# Start the application
CMD ["/entrypoint.sh"]
