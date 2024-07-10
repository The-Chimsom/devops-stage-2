FROM python:3.12.4-bookworm


WORKDIR /app

RUN apt-get update && apt-get install -y \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

COPY pyproject.toml ./

COPY poetry.lock ./

RUN pip install poetry

RUN poetry install

ENV PYTHONPATH=/app

COPY . .

EXPOSE 8000

CMD ["sh", "-c", "poetry run bash ./prestart.sh && poetry run uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload"]