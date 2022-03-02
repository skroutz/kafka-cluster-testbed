FROM --platform=linux/amd64 debian:buster

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    procps \
    curl gnupg \
    ruby

# Setup skroutz repositories
ADD skroutz-stable.list /etc/apt/sources.list.d/
RUN curl -sSL https://debian.skroutz.gr/skroutz.asc | apt-key add -

RUN apt-get update && apt-get install -y --no-install-recommends \
    kafkacat \
    rafka

ADD config.json /etc/rafka/config.json
EXPOSE 6380

ENTRYPOINT ["/usr/bin/rafka", "--config", "/etc/rafka/config.json"]
