FROM python:3.11.5

RUN apt-get update && apt-get install -y curl

RUN mkdir -p /home/python/app && \
    [ ! -d /home/python/app/.pytest_cache ] && mkdir -p /home/python/app/.pytest_cache || true && \
    [ ! -d /home/python/app/.ruff_cache ] && mkdir -p /home/python/app/.ruff_cache || true && \
    [ ! -d /home/python/app/.mypy_cache ] && mkdir -p /home/python/app/.mypy_cache || true && \
    [ ! -d /home/python/app/src ] && mkdir -p /home/python/app/src || true
COPY ./backend/pyproject.toml ./backend/poetry.lock /home/python/app/

ENV POETRY_VIRTUALENVS_CREATE=false
ENV POETRY_HOME=/home/poetry
ENV PATH=${POETRY_HOME}/bin:${PATH}
ENV PYTHONPATH="/home/python/app/src:/home/python/app/tests:${PYTHONPATH}"

RUN curl -sSL https://install.python-poetry.org | python3 -

WORKDIR /home/python/app
RUN poetry config virtualenvs.create false && \
    poetry install --no-interaction --no-root