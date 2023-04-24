# Use the official Miniconda3 base image
FROM continuumio/miniconda3:latest

# Set environment variables
ENV DEBIAN_FRONTEND=noninteractive

# Install system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    && rm -rf /var/lib/apt/lists/*

# Create a conda virtual environment
RUN conda create --name camel python=3.10

# Activate the conda environment and install pre-commit
RUN echo "conda activate camel" >> ~/.bashrc && \
    /bin/bash -c "source ~/.bashrc && \
    conda init bash && \
    conda activate camel && \
    pip install pre-commit"

# Clone the camel repository
RUN git clone https://github.com/lightaime/camel.git

# Change the working directory to the camel directory
WORKDIR /camel

# Install camel from source
RUN /bin/bash -c "source ~/.bashrc && \
    conda activate camel && \
    pre-commit install && \
    pip install -e ."

# Set the default shell to bash
SHELL ["/bin/bash", "-c"]

# Keep the container running
CMD ["tail", "-f", "/dev/null"]
