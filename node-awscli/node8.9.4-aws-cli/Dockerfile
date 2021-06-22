FROM node:8.9.4

# install aws-cli

# zip
RUN apt-get update && apt-get install -y zip && rm -rf /var/lib/apt/lists/*

# aws
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && unzip awscliv2.zip
RUN ./aws/install && aws --version

ENV VERSION=0.2.2
RUN curl -sSLO https://github.com/awslabs/aws-sam-local/releases/download/v${VERSION}/sam_${VERSION}_linux_386.tar.gz && \
    tar -C /usr/local/bin -zxvf /sam_${VERSION}_linux_386.tar.gz && \
    rm -f /sam_${VERSION}_linux_386.tar.gz

CMD ["node"]
