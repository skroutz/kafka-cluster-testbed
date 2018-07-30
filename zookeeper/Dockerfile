FROM debian:stretch

# Faster debian mirror
RUN sed -i -e 's|http://deb.debian.org|http://debian.anycast-test.mirrors.debian.org|' /etc/apt/sources.list
RUN sed -i -e 's|http://security.debian.org|http://security.anycast-test.mirrors.debian.org/|' /etc/apt/sources.list

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    procps \
    curl gnupg \
    ruby \
    openjdk-8-jre-headless \
    zookeeper

ADD zoo /usr/local/bin/zoo

EXPOSE 2181

ENTRYPOINT ["/usr/local/bin/zoo"]
