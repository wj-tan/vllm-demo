# Use the official Python image
FROM registry.access.redhat.com/ubi9/python-311:latest

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV LLM_ENDPOINT=https://ollama.molodetz.nl/v1/
ENV LLM_MODEL=mistral:instruct

# Set the working directory
WORKDIR /app

USER root
# Install system dependencies
RUN dnf update -y && \
    dnf install -y gcc gcc-c++ make redhat-rpm-config glibc-devel \
    && dnf clean all

# Install Python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY app.py .

# Expose the Streamlit port
EXPOSE 8501
USER default
# Run the Streamlit app
CMD ["streamlit", "run", "app.py", "--server.port=8501", "--server.address=0.0.0.0"]
