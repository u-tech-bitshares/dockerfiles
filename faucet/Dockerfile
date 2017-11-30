FROM python:3-alpine

WORKDIR /opt

RUN apk add --no-cache --virtual .build-tmp git gcc g++ openssl-dev linux-headers \
    && git clone -b docker --single-branch https://github.com/u-tech-bitshares/faucet.git faucet

WORKDIR faucet

COPY config.yml .
RUN pip install --no-cache-dir -r requirements.txt \
    && pip install --no-cache-dir uwsgi \
    && python manage.py install \
    && apk del .build-tmp

EXPOSE 9090

CMD [ "uwsgi", "--ini", "wsgi.ini" ]
