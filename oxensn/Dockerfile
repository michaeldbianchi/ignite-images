FROM weaveworks/ignite-ubuntu

RUN sudo curl -so /etc/apt/trusted.gpg.d/oxen.gpg \
  https://deb.oxen.io/pub.gpg \
  && echo "deb https://deb.oxen.io $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/oxen.list \
  && sudo apt update \
  && sudo apt install -y oxen-service-node

