FROM python:3.10


# Set working directory
WORKDIR /app

# Install necessary build tools and libraries
RUN apt update && apt install -y --no-install-recommends \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Install Poetry
RUN curl -sSL https://install.python-poetry.org | python3 -
ENV PATH="/root/.local/bin:$PATH"

COPY . /app

# Install dependencies
RUN poetry install

# Ensure prestart.sh is executable
RUN chmod +x ./prestart.sh

# Expose application port
EXPOSE 8000

# Start the application
CMD ["sh", "-c", "poetry run bash ./prestart.sh && poetry run uvicorn app.main:app --host 0.0.0.0"]
