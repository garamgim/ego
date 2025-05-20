FROM python:3.10

# Set working directory inside the container
WORKDIR /app

# Install Poetry package manager using pip
RUN pip install poetry

# Copy dependency files separately to cache dependencies and speed up rebuilds
COPY pyproject.toml poetry.lock /app/

# Configure Poetry to install packages in the global environment (not in a virtualenv)
RUN poetry config virtualenvs.create false && \
    poetry install --no-root

# Copy the entire project source code into the container
COPY . .

# Expose port 8000 for the FastAPI application
EXPOSE 8000

# Run the FastAPI app with Uvicorn via Poetry, binding to all interfaces on port 8000
ENTRYPOINT [ "poetry" ,"run", "uvicorn", "src.server.main:app", "--host", "0.0.0.0", "--port", "8000" ]