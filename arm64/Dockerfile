FROM ubuntu:22.04

RUN apt update
RUN apt upgrade -y
RUN apt install -y curl git jq libicu70 openjdk-17-jdk unzip wget

#Install Maven
RUN apt -y install maven

# Install Docker CLI and Docker Compose
RUN curl -fsSL https://get.docker.com -o get-docker.sh && sh ./get-docker.sh

# Install Golang
RUN apt install -y golang-go

# Also can be "linux-arm", "linux-arm64", "linux-x64".
ENV TARGETARCH="linux-arm64"

# For ARM arch exclusively
COPY ./arm64/multiarch-cap.sh ./
RUN chmod +x ./multiarch-cap.sh && ./multiarch-cap.sh

WORKDIR /azp/

COPY ./start.sh ./
RUN chmod +x ./start.sh

# Another option is to run the agent as root.
ENV AGENT_ALLOW_RUNASROOT="true"
ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-arm64
ENV JAVA_HOME_17_X64=${JAVA_HOME}
ENV GO=/usr/bin/go
ENV PYTHON=/usr/bin/python3
RUN export PATH
RUN export JAVA_HOME
RUN export JAVA_HOME_17_X64
ENTRYPOINT ./start.sh