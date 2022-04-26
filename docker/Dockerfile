FROM python:3.10-slim as base


FROM base as test
RUN pip install pytest
COPY ./docker/test_capitalize.py  /app/myapp/tests/
WORKDIR /app/myapp/tests
RUN pytest

