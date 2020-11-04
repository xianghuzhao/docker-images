FROM python:3.8-slim as builder

RUN apt-get update -y && \
    apt-get install -y gcc

RUN pip install --no-cache --upgrade pip virtualenv && \
    virtualenv /venv-devpi && \
    . /venv-devpi/bin/activate && \
    pip install --no-cache devpi-server devpi-web

FROM python:3.8-slim

COPY --from=builder /venv-devpi /venv-devpi

COPY devpi-server.yml /etc/devpi-server/devpi-server.yml

COPY entrypoint.sh /entrypoint.sh

RUN mkdir -p /data/db && \
    mkdir -p /data/secret && \
    mkdir -p /etc/devpi-server && \
    touch /data/secret/secret && \
    . /venv-devpi/bin/activate && \
    devpi-init -c /etc/devpi-server/devpi-server.yml

EXPOSE 3141

VOLUME /data

ENTRYPOINT ["/entrypoint.sh"]

CMD ["devpi-server", "-c", "/etc/devpi-server/devpi-server.yml"]
