# AWS CLI in Docker

Containerized AWS CLI on alpine to avoid requiring the aws cli to be installed on CI machines. Based on mesosphere/aws-cli. 

## Build

```
docker build -t totersapp/aws-cli .
```

Automated build on Docker Hub

[![DockerHub Badge](http://dockeri.co/image/totersapp/aws-cli)](https://hub.docker.com/r/totersapp/aws-cli/)

## Maintenance 

- The Docker image build & publish is automated by DockerHub for master commits and tags.
- The awscli and s3cmd packages have handcoded versions in the Dockerfile that need to be bumped manually.

## References

AWS CLI Docs: https://aws.amazon.com/documentation/cli/
