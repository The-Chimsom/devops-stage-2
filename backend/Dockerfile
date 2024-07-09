FROM python:3.9.19-bookworm


WORKDIR /app

RUN apt-get update && apt-get install -y \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

COPY pyproject.toml ./

COPY poetry.lock ./

RUN pip install poetry

RUN poetry install

ENV POSTGRES_USER="{user}"
ENV POSTGRES_PASSWORD="{password}"
ENV POSTGRES_SERVER="{server}"
ENV POSTGRES_PORT="{port}"
ENV POSTGRES_DB="{db}"

# Construct the final connection string using these variables
ENV DATABASE_URL="postgresql+psycopg://${PG_USER}:${PG_PASSWORD}@${PG_SERVER}:${PG_PORT}/${PG_DB}"

COPY . .

CMD ["uvicorn", "app.main:app", "--proxy-headers", "--host", "0.0.0.0", "--port", "5170"]
