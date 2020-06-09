FROM mcr.microsoft.com/vscode/devcontainers/base:ubuntu-18.04@sha256:ae58821ff1dbd726871465a7a56c9467477db23b7fd432379e8ff8020424b89d

# Node.js
RUN curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash - \
    && sudo apt-get install -y nodejs=12.16.3-1nodesource1

RUN apt-get update

# Python
RUN apt install -y software-properties-common \
    && add-apt-repository -y ppa:deadsnakes/ppa \
    && apt-get -y install --no-install-recommends python3.7=3.7.7-1+bionic1 python3-pip=9.0.1-2.3~ubuntu1.18.04.1

# OpenJDK
RUN apt-get install -y openjdk-11-jre-headless

# Juypter
RUN python3.7 -m pip install setuptools==46.1.3 \
    && python3.7 -m pip install wheel==0.34.2 \
    && python3.7 -m pip install jupyter==1.0.0 \
    && python3.7 -m pip install ipykernel \
    && python3.7 -m ipykernel install --user

# Docker
RUN apt-get install -y apt-transport-https ca-certificates curl lsb-release \
    && curl -fsSL https://download.docker.com/linux/$(lsb_release -is | tr '[:upper:]' '[:lower:]')/gpg | apt-key add - 2>/dev/null \
    && echo "deb [arch=amd64] https://download.docker.com/linux/$(lsb_release -is | tr '[:upper:]' '[:lower:]') $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list \
    && apt-get update \
    && apt-get install -y docker-ce-cli=5:19.03.8~3-0~ubuntu-bionic \
    && LATEST_COMPOSE_VERSION=1.25.5 curl -sSL "https://github.com/docker/compose/releases/download/${LATEST_COMPOSE_VERSION}/docker-compose-Linux-x86_64" -o /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/docker-compose

# PlantUML (for Juypter)
RUN apt-get install -y plantuml \
    && python3.7 -m pip install iplantuml \
    && ln -s /usr/share/plantuml/plantuml.jar /usr/local/bin/plantuml.jar

# Cleanup
RUN apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*