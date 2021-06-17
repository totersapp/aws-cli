FROM node:8.15.1-alpine

# install aws-cli
RUN apk add --no-cache \
        python3 \
        py3-pip \
    && pip3 install --upgrade pip \
    && pip3 install \
        awscli \
    && apk -v --update add git \
    && apk -v --purge del py3-pip \
    && rm -rf /var/cache/apk/*

CMD ["node"]
