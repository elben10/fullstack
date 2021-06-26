FROM python:3.8-slim

WORKDIR /app

RUN pip install --no-cache poetry && \
    poetry config virtualenvs.create false

COPY src/api/pyproject.toml src/api/poetry.lock* /app/

RUN poetry install --no-root --no-dev

COPY src/api/ /app/
COPY images/api/gunicorn_conf.py /gunicorn_conf.py

CMD gunicorn -k "uvicorn.workers.UvicornWorker" -c "/gunicorn_conf.py" "src.main:app"
