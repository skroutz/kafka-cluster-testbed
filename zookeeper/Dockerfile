FROM debian:buster

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    procps \
    curl gnupg \
    ruby \
    default-jre-headless \
    zookeeper

ADD zoo /usr/local/bin/zoo

EXPOSE 2181

ENTRYPOINT ["/usr/local/bin/zoo"]
