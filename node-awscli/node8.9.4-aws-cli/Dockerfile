FROM node:8.9.4-alpine

# install aws-cli

ENV VERSION=0.2.2

RUN apk add --no-cache curl && \
    curl -sSLO https://github.com/awslabs/aws-sam-local/releases/download/v${VERSION}/sam_${VERSION}_linux_386.tar.gz && \
    tar -C /usr/local/bin -zxvf /sam_${VERSION}_linux_386.tar.gz && \
    apk del curl && \
    rm -f /sam_${VERSION}_linux_386.tar.gz

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
