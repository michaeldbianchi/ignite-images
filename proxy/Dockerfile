FROM weaveworks/ignite-ubuntu

# Install docker
RUN apt-get update \
  && apt-get -y install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release \
  && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg \
  && echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null \
  && apt-get update \
  && apt-get -y install docker-ce docker-ce-cli containerd.io \
  && rm -rf /var/lib/apt/lists/*

# install docker-compose
RUN curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose \
  && chmod +x /usr/local/bin/docker-compose

# Setup docker-compose service
COPY ./etc/systemd/* /etc/systemd/system/
RUN ln -s /etc/systemd/system/docker-compose.service /etc/systemd/system/multi-user.target.wants/docker-compose.service \
  && ln -s /etc/systemd/system/docker-compose-reload.timer /etc/systemd/system/timers.target.wants/docker-compose-reload.timer

# Copy the app over
WORKDIR /app

COPY ./app /app
