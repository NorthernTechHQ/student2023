FROM python:3.7.12-alpine3.15

ENV PYTHONUNBUFFERED 1

COPY ./requirements.txt /requirements.txt

# Install postgres client
RUN apk add --update --no-cache postgresql-client

# Install individual dependencies
# so that we could avoid install extra packages
RUN apk add --update --no-cache --virtual .tmp-build-deps \
	gcc libc-dev linux-headers postgresql-dev
RUN pip install -r /requirements.txt

# Remove dependencies
RUN apk del .tmp-build-deps
RUN mkdir /insecure_webapp
WORKDIR /insecure_webapp
COPY ./ /insecure_webapp


# [Security] Limit the scope of user who run the docker image
# RUN adduser -D user

# USER user
