FROM python:3.6.7-alpine
LABEL maintainer="Yuriy Medvedev <medvedev.yp@gmail.com>"
ENV PYTHONUNBUFFERED 1
ENV ALPINE_VERSION=3.8
ENV DB_NAME=vespene
ENV DB_USER=vespene
ENV DB_PASS=vespene
ENV DB_HOST=vespene
ENV FILESERVING_HOSTNAME=this-server.example.com
ENV BUILDROOT="/tmp/vespene"
ENV BUILDROOT_WEB_LINK="http://not-configured-by-your-vespene-admin-yet.example.com/builds/{{ build.id }}"

RUN apk update && apk add supervisor git make postgresql-libs
RUN  mkdir -p /opt/vespene \
     mkdir -p /var/spool/vespene \
     mkdir -p /etc/vespene/settings.d/
#     git clone
WORKDIR /opt/vespene
COPY files/database.py /etc/vespene/settings.d/database.py
COPY files/workers.py /etc/vespene/settings.d/workers.py
COPY files/interface.py /etc/vespene/settings.d/interface.py
RUN git clone https://github.com/vespene-io/vespene.git  /opt/vespene
RUN apk add --virtual .build-deps gcc musl-dev postgresql-dev libffi  libffi-dev && \
    make && \
    make secrets && \
    make  collectstatic && \
    apk --purge del .build-deps
ADD https://github.com/ufoscout/docker-compose-wait/releases/download/2.4.0/wait /wait
RUN chmod +x /wait
